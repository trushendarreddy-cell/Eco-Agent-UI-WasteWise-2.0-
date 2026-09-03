# WasteWise 2.0 — 24 Hour Hackathon Build

A short, honest story of how this project came together in a single day. Built by
[shankar (@shankar791)](https://github.com/shankar791) and me.

## What we set out to build

WasteWise is an eco app that turns a mobile photo of your waste into a clear
plan: what it is, how to dispose of it, how much carbon it represents, and how
many green reward points you earn. The original idea was to make sustainability
feel less like a chore and more like a small game you play every day.

We had roughly twenty four hours, one laptop, and a public demo at the end.
That meant we had to choose carefully what was real and what was theatre.

## The shape of the project

We split the work into three folders so each piece could be built and
criticised on its own.

```
backend/                # FastAPI service: AI classification, auth, scoring, stats
cinematic-scroll/       # Next.js 16 + React Three Fiber front end
3d-rendering-frames/    # The 96 frame sequence that drives the scroll animation
```

The backend is the brain. The cinematic scroll is the face. The frame
sequence is the heart of the experience. Pulling any one of them apart
should still leave the others understandable.

## How we actually built it

### 1. The frame sequence came first

Before any code, we generated ninety six still frames of a rotating Earth
in After Effects and rendered them out at full HD. We did this before
writing a single line of front end code because we wanted to know whether
the idea was even technically feasible. Could a browser really chew
through ninety six textures and swap them at sixty frames a second while
the user scrolls?

Yes, but with a trick.

In `components/ImageSequence.tsx` we load five critical frames first
(frame zero, twenty four, forty eight, seventy two, ninety five). They
give the user something real to look at within a few hundred milliseconds.
Only after the critical set is ready do we start fetching the remaining
ninety one frames in the background. We also wired up a nearest
loaded frame fallback in the render loop, so the animation never tears
even mid load.

The lesson here was simple: perception of speed is not the same as
actual speed. Show the user something real, then quietly finish the job.

### 2. The cinematic scroll front end

The scroll experience is plain CSS plus GSAP plus React Three Fiber. There
is no magic. The body is set to five hundred viewports tall in
`app/globals.css`. A GSAP `ScrollTrigger` watches `body` from top to
bottom and writes a normalised progress number into a ref. Each animation
frame, we multiply that progress by ninety six, pick the nearest loaded
frame, and assign it as the texture on a single plane geometry.

The `CTASection` listens for a custom `scroll-complete` event that the
sequence fires when progress crosses ninety eight percent. That is how
the final overlay knows when to fade in without polling. Events, not
polls.

We also built a real `UploadPage` at `/upload` with a glassmorphic file
drop zone, client side validation, and a result card that shows the AI
output. That is the part that actually connects to the backend.

### 3. The backend

The backend is FastAPI on Python three eleven. Three layers:

- `app/api` is the HTTP edge, with thin endpoints and Pydantic schemas.
- `app/services` holds the actual logic: image classification, label
  mapping, scoring, fallback.
- `app/db` is SQLAlchemy with a connection pool tuned for production.

We deliberately split the legacy `main.py` style monolith into modules
halfway through the hackathon, because by hour ten we could no longer
find anything in the single file version. That refactor cost us an
hour. It saved us the next six.

Authentication uses bcrypt through passlib. Passwords are hashed, never
stored as plain text. Sessions are intentionally simple for the demo:
the email acts as the identity token on each request.

### 4. AI classification is hybrid

We use a pretrained MobileNetV2 from torchvision for image classification.
On its own it does not know what waste is. It knows what a banana looks
like. So we built `waste_mapper.py`, a hand curated lookup table from
ImageNet labels to our four waste categories: wet, dry, e waste,
hazardous. That table is the secret sauce.

When the model's confidence is below fifty five percent, we fall back to
keyword matching on the filename. That is honest about the model's
limits and saves us from confidently wrong predictions in front of a
live audience.

### 5. Scoring

For every upload we compute:

- carbon saved, using a per category emission factor
- tree equivalent, roughly one tree per twenty one kilograms of CO2 per year
- sustainability score, a weighted blend of base, weight, and carbon
- reward points, a function of the score with a floor of twenty

Those four numbers are returned together so the front end can show a
single coherent story instead of four disconnected stats.

### 6. Deployment shape

The Dockerfile is a two stage build. The builder stage installs PyTorch
from the CPU only index URL, then the rest of the requirements. The
final stage only carries the installed packages forward, which keeps
the runtime image small and removes the need for gcc in production.

The FastAPI app mounts the `cinematic-scroll/public` directory as static
files at `/`, so a single container serves both the API and the entire
front end. One process. One port. One deployment.

We also kept a pure HTML version of the cinematic scroll in
`cinematic-scroll/public/index.html` so the experience works even when
the user hits the raw backend URL and there is no Node runtime
available.

## Problems we actually ran into

**Texture loading made the page feel broken.** Loading ninety six
high resolution JPEGs at once locked the main thread for several
seconds. The progressive critical frame trick fixed it.

**ScrollTrigger fired before textures were ready.** If we registered
the trigger too early, the first paint was a black frame. We moved
trigger registration behind a `criticalLoaded` gate so the experience
is always smooth.

**Pydantic raised on missing optional columns.** Half the columns in
`WasteLog` were added later during the hackathon. We added safe
`ALTER TABLE` blocks wrapped in try/except so the same code works on
a fresh SQLite database and on a populated Postgres instance on
Railway. Quiet migrations beat clever migrations at two in the morning.

**MobileNetV2 confidently misclassified things.** A plastic bottle
under bad lighting became a syringe, which would have routed it to
hazardous disposal. The confidence threshold plus the keyword
fallback prevents that.

**Serving the front end from FastAPI.** We did not want to run two
services. We mounted the public directory as static files at the
root, but only after registering every API route, so `/signup`,
`/login`, and `/user/upload` are never shadowed by `index.html`.

**CORS in development.** During local testing the front end lives on
port 3000 and the backend on port 8000. We start with a permissive
CORS policy and rely on the `Authorization` header pattern rather
than cookies. For the production deploy on a single origin we lock it
down via environment variable.

**The eighteen second preloader felt dead.** We added a fake progress
bar that increments up to eighty five percent while the real work
finishes, and a phase based status message that swaps from
"Initializing" to "Loading assets" to "Almost there" based on
elapsed seconds. It is theatre, but good theatre.

**Git push kept failing because the frame folder was huge.** Adding
the ninety six frames to git produced hundreds of megabytes of
diffs. The frames are part of the product, so we kept them in git
despite the size, but we make sure the public serving path skips
git and goes straight to disk.

## What is real versus what is decoration

For the demo we were explicit with ourselves:

- The frame sequence and the cinematic scroll are real. They ship as
  part of the product, not as a marketing video.
- The AI classifier is real and runs inside the same container as
  the API. The first request after a cold start is slow because the
  model has to load. We accept that and cache the classifier as a
  module level singleton.
- The leaderboard, streak counter, weekly CO2 graph, rewards, and
  campaigns are all real and persisted in the database.
- The shop pages and merch cards in the public folder are concept
  mockups, not a checkout. We kept them because they make the
  product feel complete, but no money changes hands.

## How to run it locally

```bash
# backend
cd backend
pip install -r requirements.txt
python main_improved.py
# the API is now at http://localhost:8000
# the cinematic scroll is at http://localhost:8000/
```

```bash
# front end with hot reload
cd cinematic-scroll
npm install
npm run dev
# open http://localhost:3000
```

## Credits

Built over twenty four hours by
[shankar (@shankar791)](https://github.com/shankar791) and me. The
frame sequence was rendered by us in After Effects. The classifier
runs on MobileNetV2 weights from torchvision. Everything else is
handwritten under deadline pressure.
# DOMAIN: SUSTAINABLE MANAGEMENT

## Eco-Agent UI (WasteWise 2.0)

A short write up of the problem we tackled, the system we proposed, and the
references that anchor our thinking. Written for a hackathon pitch deck.

## 1. The Core Problem

Many major Indian cities like Hyderabad and Mumbai, and growing cities like
Khammam and Warangal, share a common problem: waste disposal is still
inconsistent despite initiatives like the Swachh Bharat Mission. India
generates over 150,000 tonnes of municipal solid waste every day, and
segregation at source remains below optimal levels in most urban areas.

The visible symptoms:

- Waste segregation at the household level is poor.
- People do not know how to dispose of specific items.
- Municipal collection systems are inefficient.
- Citizens receive no meaningful incentive to change behaviour.
- There is no proper recycling ecosystem connecting households to buyers.

### Main Causes

- No widespread awareness of sustainable waste management practices.
- No smart feedback loop that tells a citizen whether they did the right thing.
- No real-time feedback systems after disposal.
- No measurable sustainability tracking at the individual level.

## 2. The Proposed System

Eco-Agent UI (WasteWise 2.0) is a multi-agent, AI-powered sustainable
waste management ecosystem that connects citizens, municipalities, and
recyclers through intelligent guidance and predictive analytics.

It is best understood as a digital sustainability infrastructure layer
sitting on top of existing municipal systems, not a replacement for them.

## 3. The Five AI Agents

### Citizen Agent

- Uploads an image of the waste they want to dispose of.
- Receives an instant classification for the waste.
- Receives an eco-score for the action.
- Earns reward points that can later be redeemed.
- Views their personal sustainability dashboard.

### AI Classification Agent

- Maps an uploaded image to a waste category (wet, dry, e-waste, hazardous).
- Estimates the carbon impact of the disposal choice.
- Suggests the correct disposal method for the item.
- Provides a short educational explanation of why the item belongs where
  it does.

### Collection Optimization Agent

- Predicts waste generation hotspots across the city.
- Suggests optimized collection routes for the municipality.
- Reduces fuel consumption per trip.
- Lowers municipal operational cost per tonne collected.

### Municipality Agent

- Surfaces dashboard analytics for officers and ward planners.
- Breaks down area-based segregation rates.
- Tracks city-wide carbon reduction data.
- Provides policy decision insights backed by real numbers.

### Recycling Partner Agent

- Connects verified recyclers to properly sorted waste streams.
- Tracks e-waste sources through the chain of custody.
- Enables a real circular economy by closing the loop between citizen and
  recycler.

## 4. Functional Flow of the App

1. The user opens the app and uploads an image of the waste.
2. The AI Classification Agent returns an instant category:
   - Wet (food scraps, organic)
   - Dry (plastic, paper, metal, glass, cloth)
   - E-waste (mobile, laptop, electronics)
   - Toxic or hazardous (battery, chemical, paint)
3. The system then computes, for the chosen weight and category:
   - Carbon emissions saved by the correct disposal choice
   - Eco points awarded to the user
   - A sustainability score for the action
4. The aggregated data feeds into:
   - The user leaderboard for friendly competition
   - Area analytics for the municipality agent

### Hybrid Input Eco-Agent

For users without a usable photo, the app also supports a manual waste
selector. The user picks the waste type and approximate weight, and the
same scoring model still calculates the carbon impact. The agent is
deliberately input-agnostic: the model rewards the action, not the
medium.

## 5. Behavioural Engineering

Why behaviour change is the real problem:

- The problem is not a shortage of dustbins. It is a shortage of motivation.
- There is no instant feedback after a citizen disposes of something.
- There is no visible impact they can point to and feel good about.
- There is no social pressure to do better.

Even campaigns like Swachh Bharat Mission lean heavily on awareness, but
awareness alone does not sustain habits. The system has to reward the
habit in a way the citizen can see, share, and feel.

## 6. Carbon Impact Visualization

Instead of telling a user "You segregated waste", the app says:

> "You reduced 1.2 kg CO2 - equivalent to planting 2 trees."

When impact becomes tangible, people act. This single line of copy is the
centre of gravity for the user experience, and it is also the unit of
truth that the municipality dashboard reports upward.

## 7. Sustainability Metrics Model

We define a composite Sustainability Score (SS) that combines the three
levers we can actually influence:

```
SS = (Segregation Accuracy × 0.4)
   + (Participation Frequency × 0.3)
   + (Carbon Reduction × 0.3)
```

The weights are deliberate. Accuracy matters most because a wrongly
sorted item contaminates the entire batch. Frequency matters because the
goal is to form a daily habit. Carbon matters because it is the only
metric the wider climate conversation can compare against.

This index gives us a quantitative evaluation for each user and a way to
compare neighbourhoods without leaking personally identifiable data.

## 8. Institutional and Deployment Relevance

The system aligns with:

- Central Pollution Control Board municipal waste reporting frameworks.
- Greater Hyderabad Municipal Corporation urban management models.
- National sustainability missions under the Ministry of Environment,
  Forest and Climate Change.

Deployment is staged so that risk is low at every step:

- Campus-level pilot (a single college or IT park).
- Ward-level rollout inside a municipal zone.
- City-level integration with civic services.
- Smart city integration with traffic, lighting, and bin sensors.

Each stage is independently useful, so we never depend on a later stage
to justify the earlier one.

## 9. References

1. Central Pollution Control Board (CPCB)
   - Annual Reports on Municipal Solid Waste
     https://cpcb.nic.in/annual-report/
   - Solid Waste Management Reports
     https://cpcb.nic.in/municipal-solid-waste/

2. Solid Waste Management Rules, 2016 (Official Government Notification)
   - https://moef.gov.in/wp-content/uploads/2017/08/SWM_2016.pdf
   - Ministry of Environment, Forest and Climate Change

3. Swachh Bharat Mission (Urban), Official Portal
   - https://swachhbharatmission.gov.in/sbmcms/index.html

4. Greater Hyderabad Municipal Corporation (GHMC)
   - https://www.ghmc.gov.in/

5. IPCC Climate Reports
   - https://www.ipcc.ch/reports/
   - Intergovernmental Panel on Climate Change
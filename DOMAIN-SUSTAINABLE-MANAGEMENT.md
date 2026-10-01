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

## Additional References

### Government and Policy

6. Ministry of Housing and Urban Affairs (MoHUA), Annual Reports
   - https://mohua.gov.in/
   - Source for city-level urban sustainability metrics and Smart Cities
     Mission outcomes.

7. National Institute of Urban Affairs (NIUA)
   - https://niua.org/
   - Research and policy briefs on Indian solid waste management.

8. NITI Aayog, Sustainable Development Goals Index Report
   - https://niti.gov.in/sdg-india-index/
   - SDG 11 and 12 indicators relevant to waste and sustainable cities.

9. Plastic Waste Management Rules, 2016 (and 2022 Amendment)
   - https://moef.gov.in/wp-content/uploads/2017/08/PWM_2016.pdf
   - https://moef.gov.in/wp-content/uploads/2022/07/Plastic-Waste-Management-Amendment-2022.pdf
   - Extended Producer Responsibility and single-use plastic phase-out.

10. E-Waste Management Rules, 2022
    - https://moef.gov.in/wp-content/uploads/2022/07/E-Waste-Management-Rules-2022.pdf
    - Producer responsibility for electronics and battery waste streams.

11. Construction and Demolition Waste Management Rules, 2016
    - https://moef.gov.in/wp-content/uploads/2017/08/CDWM_2016.pdf
    - Material recovery targets and reporting structure.

12. Bio-Medical Waste Management Rules, 2016
    - https://moef.gov.in/wp-content/uploads/2017/08/BMW_2016.pdf
    - Categorisation and treatment standards for hazardous clinical waste.

13. Swachh Bharat Mission (Gramin), Official Portal
    - https://swachhbharatmission.gov.in/sbmcms/index.html
    - Rural counterparts and behaviour change campaigns.

14. Smart Cities Mission, Official Portal
    - https://smartcities.gov.in/
    - Indicator framework that the Municipality Agent can map onto.

15. India State of Forest Report, Forest Survey of India
    - https://fsi.nic.in/forest-report-2021
    - Tree carbon sequestration coefficients used for the trees-equivalent
      metric in the citizen dashboard.

### International Benchmarks

16. World Bank, What a Waste 2.0 Report
    - https://datatopics.worldbank.org/what-a-waste/
    - Global solid waste generation, composition, and management data.

17. UN Environment Programme (UNEP), Waste Management Resources
    - https://www.unep.org/explore-topics/resource-efficiency
    - Lifecycle and circular economy framing.

18. United Nations Sustainable Development Goals
    - https://sdgs.un.org/goals
    - Specifically SDG 11 (Sustainable Cities), SDG 12 (Responsible
      Consumption and Production), and SDG 13 (Climate Action).

19. OECD, Environment at a Glance Indicators
    - https://www.oecd.org/environment/environment-at-a-glance/
    - Comparable per-capita waste and recycling indicators.

20. Ellen MacArthur Foundation, Circular Economy Reports
    - https://ellenmacarthurfoundation.org/publications
    - Model for the Recycling Partner Agent.

### Academic Research

21. Hoornweg, D. and Bhada-Tata, P. (2012), "What a Waste: A Global
    Review of Solid Waste Management", Urban Development Series Knowledge
    Papers, World Bank.
    - https://openknowledge.worldbank.org/handle/10986/17388

22. Wilson, D.C., Velis, C. and Cheeseman, C. (2015), "Role of Informal
    Sector Recycling in Waste Management in Developing Countries", Habitat
    International, 49, pp. 402-412.

23. Ferronato, N. and Torretta, V. (2019), "Waste Mismanagement in
    Developing Countries: A Review of Global Issues", International Journal
    of Environmental Research and Public Health, 16(6), 1060.

24. Kaza, S., Yao, L., Bhada-Tata, P. and Van Woerden, F. (2018), "What a
    Waste 2.0: A Global Snapshot of Solid Waste Management to 2050", World
    Bank Group.

25. Marshall, R.E. and Farahbakhsh, K. (2013), "Systems Approaches to
    Integrated Solid Waste Management in Developing Countries", Waste
    Management, 33(4), pp. 988-1003.

### Datasets and Open Data

26. World Bank Open Data, Waste Generation Indicators
    - https://data.worldbank.org/topic/environment

27. UN Stats, Environment Indicators
    - https://unstats.un.org/unsd/envstats/

28. Our World in Data, Plastic Pollution
    - https://ourworldindata.org/plastic-pollution

29. OpenStreetMap, for the Collection Optimization Agent routing layer
    - https://www.openstreetmap.org/

30. Kaggle, Waste Classification Dataset (trashNet style)
    - https://www.kaggle.com/datasets/techsash/waste-classification-data
    - Reference dataset shape for the AI Classification Agent.

### Technology and Implementation

31. FastAPI Documentation
    - https://fastapi.tiangolo.com/

32. Next.js Documentation
    - https://nextjs.org/docs

33. React Three Fiber Documentation
    - https://docs.pmnd.rs/react-three-fiber/

34. GSAP ScrollTrigger
    - https://gsap.com/docs/v3/Plugins/ScrollTrigger/

35. PyTorch and torchvision Documentation
    - https://pytorch.org/docs/stable/index.html
    - Source for MobileNetV2 and the underlying image classification model.

36. SQLAlchemy 2.0 Documentation
    - https://docs.sqlalchemy.org/en/20/

37. PostgreSQL Documentation
    - https://www.postgresql.org/docs/

38. Docker Documentation
    - https://docs.docker.com/

40. India Digital Public Infrastructure, Open Network for Digital Commerce
    (ONDC) and India Stack
    - https://www.india.gov.in/spotlight/digital-india
    - Background on identity and consent flows relevant to citizen agents.
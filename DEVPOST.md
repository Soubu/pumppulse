# Devpost submission: copy and paste into each field

## Project name
PumpPulse

## Tagline (short description)
Water points sit broken for weeks because nobody tells the repair team. PumpPulse loads the real wells, taps and tanks for any place on Earth, lets anyone report a breakdown by plain SMS, and gets the worst fixed first.

## Project description

### 60-second tour for the judge
1. Open **https://soubu.github.io/pumppulse/**. It starts in an instant offline demo district.
2. **Tap a pulsing red dot** to see how many people it serves, how long it's been dry, and the walk to the nearest working water point.
3. Open **SMS line** and tap `BROKEN`. Watch the map turn red. Switch the language to **BM** and try `AIR KOTOR`.
4. Open **Mechanics** → **Repair…** → **Mark fixed**. The pump turns blue.
5. Open **District** and drag the simulator from 30 days to 3.
6. *(Optional, needs up to a minute to load)* Tap the 📍 button → **Ranau, Sabah** to see real OpenStreetMap data, and add a missing water point.

### In one sentence
PumpPulse turns the people who use a water pump into its alarm system: they report a breakdown from any phone, and mechanics get a queue ranked by how many people are going without water.

### Inspiration
1 in 4 people on Earth still lacks safely managed drinking water (WHO/UNICEF, 2025). What surprised us is that a lot of the problem isn't missing infrastructure. The infrastructure exists and is broken. Across rural sub-Saharan Africa, more than 184 million people depend on handpumps, and research estimates about **one in four is not working at any moment** (Foster et al., 2020). Most could be fixed in an afternoon with a cheap spare part. They stay broken for weeks because nobody tells the mechanic. Meanwhile families, mostly women and girls, walk kilometres to the next working pump.

It isn't only an African problem. Here in Malaysia, the National Audit Report 2024 found only 61% of rural Sabah has treated-water coverage, and about 39% of rural households in Sarawak lack treated or safe water. Many of those villages depend on gravity-feed systems and tanks that nobody monitors. Families in Sandakan have had water meters since 2010 but almost no water. Villagers in Beluran drew water from rivers with crocodiles during a drought. In every case the community knew long before anyone who could fix it. So we built PumpPulse to work wherever someone needs it, starting with home.

Then we found the evidence that speed is what matters. In Kenya, University of Oxford researchers fitted pumps with sensors that alert a mechanic the moment a pump breaks. **Repair times fell from about 30 days to under 3.** Most of the delay had never been the repair itself. It was the weeks before anyone found out. A sensor in every pump is expensive, though. Almost everyone near a pump already has a phone. So we asked: can people be the sensor?

### What it does
- **Works anywhere, on real data.** Search any town, for example Ranau in Sabah or Kitui in Kenya, or use your location. PumpPulse loads the real wells, public taps, springs, gravity-feed intakes and tanks mapped in OpenStreetMap. Each starts as *"not yet reported"*, because only the community can say whether it works. Missing water points can be added with a tap. The interface switches language for the country (Bahasa Melayu for Malaysia, Kiswahili for East Africa).
- **Report in seconds, from any phone.** Every pump carries an ID plate (PumpPulse generates a printable one). Villagers tap the pump on the live map, or **text it from a basic phone**: `KV-112 BROKEN`. The SMS line understands English and Kiswahili (`KV-112 MAJI MACHAFU` = dirty water), and replies with the nearest working pump plus boil-water advice when the water is contaminated.
- **See the human cost.** Tap a broken pump and the map draws the walk to the nearest working one, with how many people are affected, days without water, and walking hours lost per day.
- **Trust the data.** A single report is flagged as unconfirmed, and two or more make it confirmed. People can also text `WORKS` so the map doesn't go stale.
- **Fix what matters first.** Mechanics get one queue ranked by *people served × distance to the next working pump × days down × severity*. Contaminated water ranks higher. They take a job, log the part replaced, and the dot turns blue.
- **Prove the payoff.** The district dashboard opens with the answer (*"Fix KV-121, KV-134, KV-145 first: 2,120 people get water back…"*). It includes a **repair-time simulator** calibrated to real data. Dragging average repair time from 30 days to 3 cuts people without water on an average day in our demo district from **5,643 to 728**.
- **Google Maps integration:** every water point opens in Google Maps, with walking directions to the nearest working source.
- **Three languages:** English, Bahasa Melayu and Kiswahili, and the SMS line understands all three (`RAN-004 ROSAK`, `KV-112 MBOVU`). An **offline demo district** works with no internet.

### Who it's for
Rural communities that rely on handpumps, the local mechanics who maintain them, and district water officers or NGOs responsible for keeping water flowing.

### What makes it different
Sensor systems such as Smart Handpumps detect failures automatically, but they need a device and a SIM in every pump. Water-point surveys show where pumps are, but only as a snapshot taken once a year. PumpPulse needs **no hardware** and **no new survey**. It builds on open map data that already exists worldwide, adds a live community status, and turns each report straight into a ranked repair job.

### SDG alignment
- **SDG 6.1**: universal access to safe drinking water. Fixing broken pumps is the fastest, cheapest way to restore safe water.
- **SDG 6.b**: community participation in water management. Villagers become the monitoring network.
- **SDG 5**: reduces the water-collection burden that falls mostly on women and girls.
- **SDG 3.9**: contamination is prioritised and comes with boil-water guidance.

### How we built it
A single-file web app in vanilla HTML, CSS and JavaScript. Real places use **Leaflet** with **OpenStreetMap** tiles. Water points come live from the **Overpass API** and place search from **Nominatim**. Points are classified by OSM tags (`man_made=water_well`, `water_tap`, `natural=spring`, `storage_tank` + `content=water`, …) and given short plate IDs such as `RAN-012`. Each is linked to its nearest village, with distances calculated by the haversine formula. The offline demo district, pump plates and charts are hand-drawn SVG. State persists in localStorage. The simulator uses a steady-state breakdown model: share of pumps broken = λT / (1 + λT), with λ calibrated so that 30-day repairs give the observed 25%. We tested every flow with Playwright in headless Chrome at desktop and phone sizes. The demo video was recorded from that same automated walkthrough.

### Challenges
- Designing a priority score that is fair *and* explainable. We modelled the extra walking explicitly, and every queue card shows its inputs.
- Being honest about impact. Rather than inventing numbers, we built the simulator on two published figures (1 in 4 broken, and the 30 days to 3 days repair-time result) and labelled every assumption in the app.

### Limitations (and how we'd handle them)
- **False reports:** single reports are flagged as unconfirmed, and "It works" replies clear stale problems.
- **Silent pumps:** pumps nobody has confirmed recently would be scheduled for a check visit.
- **Money:** PumpPulse makes repair budgets go further, but mechanics and parts still need funding.
- **Map coverage varies:** OSM is incomplete in places, so the app lets anyone add missing points, and people served start as estimates by type until edited.
- **This version is local:** reports live in one browser and the SMS line is simulated. "Simulate a week of reports" exists for demos, and every simulated report is labelled.

### What's next
Load real water-point records (government MIS or the Water Point Data Exchange), connect a real SMS gateway (e.g. Africa's Talking), move to a shared database so everyone sees the same live map, and pilot with one district's mechanics.

*Map data © OpenStreetMap contributors (ODbL). The offline demo district is fictional. Sources: Foster et al. (2020), Int. J. Water Resources Development; WHO/UNICEF JMP 2025; UKRI / University of Oxford, Smart Handpumps; National Audit Report 2024 (via NST); DayakDaily / JBALB Sarawak.*

*Built by Soubu (Malaysia).*

## Built with
html5, css3, javascript, leaflet, openstreetmap, overpass-api, nominatim, google-maps, svg, localstorage, github-pages, playwright, ffmpeg

## Try it out links
- Live demo: https://soubu.github.io/pumppulse/
- Source code: https://github.com/Soubu/pumppulse

## Video
`PumpPulse-demo.mp4` (84 seconds, captioned) shows the core loop in the demo district. **Best option:** after deploying, record a new version with your voice. Search "Ranau, Sabah", show the real water points, send `RAN-0xx ROSAK`, fix it as a mechanic, and finish on the simulator. Upload it to YouTube as Unlisted.

# HeatShield

**A heat warning that is about you, not your city.**
Made for people who work outside.

**Live demo:** <https://kruthikay247.github.io/heatshield/>
**Demo video:** <PASTE YOUR VIDEO LINK HERE>
**Team:** <KRUTHIKA Y>

## The problem

Delivery riders and other outdoor workers can spend hours in the sun with little water and no real break. Weather apps only describe the city. Heat illness creeps in quietly, and one of its first signs is confusion, which stops people from deciding to rest. Nobody tells them to stop.

## The solution

HeatShield keeps an eye on the heat around you and how hard you are working, then boils it down to one simple signal: **Fine**, **Slow down**, or **Stop now**.

On **Stop now** the phone vibrates, speaks a warning, and points to the closest shade and water.

What makes it different:
- It is personal: strain is scored per worker, not per city.
- It runs on an ordinary phone, with no smartwatch needed.
- The worker owns it. No employer is required.
- Scoring is designed to run on the device, so it works without signal and personal data stays on the phone.

## What this MVP does

| Feature | Status in this MVP |
|---|---|
| Heat strain score (0-100) from five readings | Working |
| Fine / Slow down / Stop now signal | Working |
| Vibration and spoken alert on Stop now | Working (vibration needs a phone) |
| Nearest-shade prompt | Simulated (fixed "200 m" text) |
| SOS button | Stub (shows a message, sends nothing) |
| Anonymous hotspot map | Simulated (dots added in the browser only) |
| "Run a shift demo" button | Working, plays a hot shift in about 35 seconds |

### How the score works

The score adds four parts, capped at 100:

1. **Environment (up to 45):** heat index from temperature and humidity (Rothfusz formula).
2. **Effort (up to 25):** heart rate above 90 bpm.
3. **Exposure (up to 15):** hours in the sun, up to 8.
4. **Hydration (up to 15):** water drunk compared with about 0.5 L per hour in the sun.

Below 35 is **Fine**, 35 to 59 is **Slow down**, and 60 or more is **Stop now**.

These thresholds are a first guess for demonstration. They are not medical advice and have not been clinically validated.

## Honest scope: what is not built yet

- **Sensors:** the ESP32 clip (BME280 + MAX30102) is planned. In this MVP the readings are set with sliders.
- **Model:** the planned TensorFlow Lite model is not trained yet. This MVP uses the rule-based formula above as a placeholder.
- **Live weather:** the Open-Meteo API is planned but not connected in this hosted demo.
- **Shade and water finder:** planned, not connected.
- **Backend and dashboard:** Supabase and a React + Leaflet hotspot dashboard are planned. Hotspot dots here live in the browser only.

## Run it locally

No install or build step.

1. Download or clone this repo.
2. Open `index.html` in any modern browser.

Or serve it: `python3 -m http.server 8000` and open http://localhost:8000.

Best viewed at phone width (in Chrome press F12, then Ctrl+Shift+M).

## Tech stack

- **MVP:** plain HTML, CSS and JavaScript in one file (`index.html`), using the browser's Vibration and Speech Synthesis APIs.
- **Planned:** Flutter, ESP32 with BME280 and MAX30102, Python + TensorFlow Lite, Open-Meteo, Supabase, React + Leaflet.

## Credits and originality

All code in `index.html` was written for this project. Third-party items used:

- Fonts: Fraunces, Inter and Caveat via Google Fonts (SIL Open Font License).
- Heat index: the public Rothfusz regression used by the US National Weather Service.
- Built with AI assistance from Claude (Anthropic) for the MVP code and documentation.

No other third-party code is included.

## Roadmap

- Weeks 1-2: talk to riders and site workers, read heat-stress guidelines, decide alert rules.
- Weeks 3-5: build the sensor clip, train and test the strain model on open data.
- Weeks 6-8: build the Flutter app with live score, alerts, SOS and hotspot map.
- Weeks 9-10: pilot with volunteers and fix what breaks.

## Safety notice

HeatShield is a prototype. It does not replace medical advice or emergency services. If someone shows signs of heat stroke (confusion, hot dry skin, fainting), call emergency services immediately.

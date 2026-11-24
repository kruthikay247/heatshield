# HeatShield

**A heat warning that is about you, not your city.**
Made for people who work outside.

- **Live demo:** <https://kruthikay247.github.io/heatshield/>
- **Demo video:** <https://drive.google.com/file/d/1JX6_mq7N8hWXZYNFRR7uXaqW0tp-Z_Zi/view?usp=sharing>
- **Technical documentation:** [TECHNICAL_DOCS.md](TECHNICAL_DOCS.md)
- **Team:** <kruthikay.24cse>

## The problem

Delivery riders and other outdoor workers can spend hours in the sun with little water and no real break. Weather apps only describe the city. Heat illness creeps in quietly, and one of its first signs is confusion, which stops people from deciding to rest. Nobody tells them to stop.

## The solution

HeatShield combines the heat around you with how hard you are working and boils it down to one signal: **Fine**, **Slow down**, or **Stop now**.

On **Stop now** the phone vibrates, speaks a warning, and starts a rest timer.

What makes it different:
- Personal: strain is scored per worker, not per city.
- Runs on an ordinary phone. No smartwatch or employer needed.
- Scoring happens on the device, so personal data stays on the phone.

## Features

| Feature | Status |
|---|---|
| Heat strain score (0-100) and Fine / Slow down / Stop now signal | Working |
| Explanation of the three biggest drivers of the score | Working |
| Live weather from Open-Meteo (temperature and humidity) | Working on the hosted link, needs location permission |
| Bluetooth heart-rate sensor support (standard BLE service) | Built, not yet tested with a real device |
| Personal profile: helmet, new to heat, age 45+ (saved on the phone only) | Working |
| Water log (+250 ml) and automatic time-in-sun counter | Working |
| Vibration and spoken alert on Stop now | Working (vibration needs a phone) |
| 10-minute rest timer | Working |
| Strain history graph with threshold lines | Working |
| Shift demo (plays a hot shift in about 35 seconds) | Working |
| Anonymous hotspot map | Simulated (dots live in the browser only) |
| SOS button | Stub (shows a message, sends nothing) |

## How the score works

Score = environment (0-45) + effort (0-25) + exposure (0-15) + hydration (0-15) + profile modifiers, capped at 100.

Below 35 is **Fine**, 35 to 59 is **Slow down**, and 60 or more is **Stop now**. Full details are in [TECHNICAL_DOCS.md](TECHNICAL_DOCS.md).

These thresholds are a first version for demonstration. They are not medical advice and have not been clinically validated.

## Architecture

Inputs (Open-Meteo weather, Bluetooth heart rate, manual sliders, worker profile) feed an on-device scoring engine. The engine drives the signal, the explanation and the alerts. A diagram, the full tech stack and the APIs are in [TECHNICAL_DOCS.md](TECHNICAL_DOCS.md).

## What is not built yet

- ESP32 sensor clip (BME280 and MAX30102). Heart rate currently comes from sliders or a Bluetooth heart-rate device.
- Trained TensorFlow Lite model. The prototype uses a rule-based formula.
- Backend (Supabase) and React + Leaflet dashboard. Hotspot dots are local.
- Shade and water finder, and real SOS messages.
- Flutter app for Android and iOS.

## Run it

No install or build step.

1. Download or clone this repo.
2. Open `index.html` in a browser, or run `python3 -m http.server 8000` and open http://localhost:8000.

Live weather and Bluetooth need HTTPS, which the hosted link provides. Best viewed at phone width (Chrome: F12, then Ctrl+Shift+M).

## Tech stack

- **Prototype:** HTML, CSS and JavaScript in one file (`index.html`), Open-Meteo API, Geolocation, Web Bluetooth, Vibration and Speech Synthesis APIs, localStorage, GitHub Pages.
- **Planned:** Flutter, ESP32 with BME280 and MAX30102, Python and TensorFlow Lite, Supabase, React and Leaflet.

## Credits and originality

All code in `index.html` was written for this project. Third-party items used:

- Open-Meteo for weather data.
- Fonts: Fraunces, Inter and Caveat via Google Fonts (SIL Open Font License).
- Heat index: the public Rothfusz regression used by the US National Weather Service.
- Built with AI assistance from Claude (Anthropic) for the prototype code and documentation.

No other third-party code is included.

## Roadmap

1. Train a model on open heat-stress data and compare it with the rule-based baseline.
2. Build and calibrate the ESP32 sensor clip.
3. Build the Flutter app with background monitoring and offline mode.
4. Connect Supabase and a Leaflet hotspot dashboard.
5. Add nearby shade and water points.
6. Pilot with delivery riders and tune thresholds from their feedback.

## Safety notice

HeatShield is a prototype. It does not replace medical advice or emergency services. If someone shows signs of heat stroke (confusion, hot dry skin, fainting), call emergency services immediately.

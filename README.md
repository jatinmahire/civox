# Civox — Your Neighborhood, Your Voice

Civox is a community-powered platform that helps neighbors report and resolve local problems — together. Speak up about a pothole, a broken streetlight, or overflowing trash. When enough voices come together, things actually get fixed.

🌐 **Live Demo:** [https://jatinmahire.github.io/civox/](https://jatinmahire.github.io/civox/)  
📍 **Demo Area:** Dehradun, Uttarakhand, India

---

## The Problem

Civic complaints are scattered across phone calls, WhatsApp messages, social media, and municipal portals. Many people report the same issue separately, making it hard for public-service teams to see what matters most.

Civox brings those fragmented voices together into one clear picture.

---

## How It Works

```
You report a problem (voice or text)
       ↓
Your words are transcribed automatically
       ↓
We figure out the category, location & urgency
       ↓
Similar reports from neighbors are grouped together
       ↓
The issue shows up on a live map
       ↓
Public-service teams take action
       ↓
You can track the fix
```

---

## What's Real vs. What's Simulated

To keep things transparent, here's what's fully working in this prototype and what's shown for demonstration:

| Feature | Current Status | Production Plan |
|---|---|---|
| **Voice Input** | **Working** — Live WebSocket + fallback to browser speech + 1-tap demo prompts | Server-side proxy with enterprise auth |
| **Speech Transcription** | **Working** — Speechmatics Realtime (~175ms latency, confidence scores, language detection) | Production Speechmatics feed |
| **Problem Categorization** | **Working** — Rule-based engine for category, landmark, severity, spam detection | Expanded NLP/ML entity extraction |
| **Duplicate Detection** | **Working** — Groups reports by category, landmark & proximity with clear explanations | Spatial DB clustering (PostGIS) |
| **Interactive Map** | **Working** — Leaflet.js + OpenStreetMap + density heatmap | Vector tiles + municipal GIS overlays |
| **Location Lookup** | **Working** — OpenStreetMap Nominatim with neighborhood fallback | Enterprise geocoding service |
| **Resident & Team Workflows** | **Working** — Report, corroborate, update status (Open → In Progress → Fixed) | Enterprise RBAC |
| **Background Activity** | **Simulated** — Periodic reports & resolutions for demo purposes | Real community traffic |
| **User Accounts** | **Demo personas** — 1-click switcher, no passwords needed | OAuth / Google Sign-In |
| **Push Notifications** | **Simulated** — Service Worker registered | Web Push + SMS/WhatsApp |
| **Data Storage** | **Working** — Browser localStorage with reset option | PostgreSQL / PocketBase |

> **Note:** Civox comes pre-configured with a built-in Speechmatics API key for live microphone streaming out of the box, with seamless browser fallback.

---

## Key Features

- **Report by voice or text** — just describe what you see
- **Live transcription** with confidence scores and language detection
- **English and Hinglish support** — speak naturally in either
- **Smart categorization** — Road Safety, Cleanliness, Lighting, Water & Sewage, Traffic
- **Landmark detection** — recognizes local streets and intersections
- **Duplicate grouping** — similar reports get combined, with clear reasoning shown
- **Community backing** — neighbors can "+1" an existing report
- **Live map** — see what's happening in your area at a glance
- **Privacy-first** — your exact location is never shared publicly
- **Full issue lifecycle** — Open → In Progress → Fixed
- **Officer dashboard** — public-service teams can triage and update status
- **WhatsApp sharing & PDF export**
- **Works on mobile** — responsive design throughout
- **Keyboard shortcut** — press `R` to quickly report an issue

---

## Speechmatics Integration

Voice input is powered by Speechmatics Realtime WebSocket API:

- **Live streaming** at 16kHz PCM with ~175ms latency
- **Model options:** Enhanced (best accuracy), Standard (fastest), Melia 1 (multilingual preview)
- **Hinglish support** — handles code-switching between English and Hindi naturally
- **Telemetry display** — shows confidence, latency, and language detection in real-time
- **Graceful fallback** — if no API key is provided, browser speech recognition and demo prompts kick in automatically

---

## Problem Categorization

When you describe an issue, Civox automatically extracts:
- **Category** (Road Safety, Cleanliness, etc.)
- **Location** (street names, landmarks)
- **Urgency level**
- **Spam risk** (filters out gibberish)

Example output from a voice report:
```json
{
  "category": "ROAD SAFETY",
  "landmark": "Rajpur Road",
  "severity": "High",
  "hazard": "Vehicle accident risk",
  "spamRisk": "Low"
}
```

---

## How Grouping Works

When multiple people report the same issue, Civox explains exactly why they were combined:

- ✓ **Same category:** Road Safety
- ✓ **Same area:** Rajpur Road / Clock Tower junction
- ✓ **Close together:** within ~120m–180m
- ✓ **Multiple witnesses:** confirmed by independent reports

No guessing — you can always see why reports were grouped.

---

## Demo Accounts

Try different perspectives using the built-in account switcher:

| Name | Role | Area |
|---|---|---|
| **Rakshan Sharma** | Resident | Rajpur Road, Dehradun |
| **Arav Sharma** | Resident | Ballupur Chowk, Dehradun |
| **Snehal Raj** | Public-Service Officer | Nagar Nigam Dehradun |

> No real credentials needed. Switch instantly from the profile menu. Guests can browse freely without signing in.

---

## Try It Out

1. Open the [Civox Live Demo](https://jatinmahire.github.io/civoxnow/).
2. Click **Try a demo** or **Report a problem**.
3. Pick a demo prompt (e.g., "Pothole Rajpur Rd") or speak/type your own.
4. Watch the transcription happen in real-time.
5. Submit the report and see it appear on the map.
6. Open the grouped issue to see how reports were combined.
7. Click **+1 Add my voice** to back an existing report.
8. Switch to the **Officer** account (Snehal Raj) to update issue status.
9. Mark an issue as **Fixed** and see it move to the resolved section.

---

## Privacy & Safety

- **Your location is approximate** — exact GPS is never stored or shown publicly
- **Single reports need backup** — marked as "Needs Verification" until corroborated
- **No personal data collected** — the demo doesn't store or transmit private credentials
- **Spam filtering** — built-in checks for gibberish and repetitive input

---

## Built With

- **Frontend:** HTML5, CSS3, Vanilla JavaScript (ES6+)
- **Speech:** Speechmatics Realtime + Web Speech API fallback
- **Maps:** Leaflet.js + OpenStreetMap + Leaflet-heat
- **Geocoding:** Nominatim (OpenStreetMap) with local fallback
- **Storage:** Browser localStorage
- **Hosting:** GitHub Pages

---

## Run Locally

```bash
git clone https://github.com/jatinmahire/civoxnow.git
cd civoxnow
```

Start a local server:
```bash
# Python
python -m http.server 4173

# Node.js
npx serve . --listen 4173
```

Open `http://localhost:4173` in your browser.

> **Tip:** Microphone and location features work best on `localhost` or HTTPS.

---

## Tests

Civox includes an automated test suite covering HTML structure, speech wiring, NLP parsing, clustering, state management, and role guards:

```bash
node test_crowdfix.js
```

**Latest Results:**
```
────────────────────────────────────────────────────────────
RESULTS: 269 passed, 0 failed
🎉 All tests passed! Civox is ready.
────────────────────────────────────────────────────────────
```

---

## Project Structure

```
civox/
├── index.html          # Main page — dashboard, map, modals
├── styles.css          # Design system — clean, warm, responsive
├── app.js              # Core logic — parser, clustering, speech, state
├── config.example.js   # Template for API key settings
├── sw.js               # Service Worker for notifications
├── test_crowdfix.js    # Automated test suite (269 tests)
└── README.md           # This file
```

---

## What's Next

This prototype shows what's possible on the client side. For production:

- **Municipal integration** — direct sync with city ERPs and helpline APIs
- **Phone-call reporting** — IVR/SIP for non-smartphone users
- **More languages** — Hindi, Kannada, Tamil, Telugu, and more
- **Photo evidence** — camera capture with GPS verification and privacy blurring
- **Proper auth** — OAuth 2.0 with government SSO
- **Smart routing** — ML-driven dispatch to the right ward engineer

---

## Vision

Civox turns scattered complaints into organized community evidence — and turns that evidence into action. When neighbors speak up together, cities listen.

---

## Credits

Powered by:
- [Speechmatics](https://www.speechmatics.com/)
- [Leaflet](https://leafletjs.com/)
- [OpenStreetMap](https://www.openstreetmap.org/)

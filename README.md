# Bolt Trip Planner — Tallinn

A lightweight intermodal route planner for Tallinn, Estonia. Enter a start 
and end location and get a suggested route combining a **Bolt Scooter**, 
**public transit**, and a **Bolt Ride** — with estimated time and cost for 
each leg of the journey.

Built as a product thinking exercise for the **Bolt Product Builder 
Programme 2026** application.

---

## 💡 The Idea

Tallinn has great public transport but getting door-to-door still requires 
switching between multiple apps and figuring out connections manually. 
This tool chains all three modes — scooter, tram/bus, Bolt ride — into a 
single suggested route, solving the last-mile problem in one place.

This is a simplified prototype of what a **Live Intermodal Route Optimizer** 
could look like inside the Bolt app — a feature concept I developed based 
on my own experience as a regular Bolt user in Tallinn.

---

## 🚀 Live Demo

👉 **[bolt-trip-planner.vercel.app](#)**  
*(replace with your actual Vercel URL)*

**Try these routes:**
| From | To | Result |
|------|----|--------|
| Mustamäe tee 149 | Bolt HQ | Mustamäe → Bolt HQ route (26 min, €6.00) |
| Anything else | Anywhere | Default Tallinn route (24 min, €5.70) |

---

## 🛠️ How It Was Built

Built entirely using **Google Antigravity IDE** — Google's agent-first 
development platform powered by Gemini 3, launched November 2025. 
No prior knowledge of the full stack was needed — I described what I 
wanted, iterated on the output, and shaped it into a working product.

**Tech stack:**
- Single `index.html` — no frameworks, no dependencies, no build step
- Vanilla HTML, CSS, JavaScript
- Bolt brand colors (`#34D186`), mobile-first, dark theme

**Key implementation details:**
- `pickRoute(start, end)` — detects which route to serve based on 
  case-insensitive keyword matching on user input
- `renderResults(route, start, end)` — dynamically builds leg elements 
  and triggers staggered CSS entrance animations (300ms apart)
- `setLoading(on)` — disables button and shows spinner during the 
  2-second simulated planning delay
- `esc(str)` — sanitizes all user input before injecting into the DOM

**Version:** 1.0.0  
**Lines of code:** ~370  
**Build time:** ~3 hours with AI assistance

---

## 🔌 API Note — Why Routes Are Hardcoded

The original plan was to connect a live AI API to generate dynamic routes 
for any address in Tallinn. Two options were attempted:

**Option 1 — Anthropic Claude API**
- Signed up at console.anthropic.com
- Free tier requires billing information to activate
- Not available during development

**Option 2 — Google Gemini API**
- Tried via Google AI Studio (aistudio.google.com)
- Also requires billing to activate even on free tier
- Not available during development

**The pragmatic decision:**  
Rather than shipping a broken app or a fake loading screen, I hardcoded 
two realistic, accurate Tallinn routes based on real tram lines, real stops, 
and real approximate costs. The app still works, looks real, and 
demonstrates the product concept clearly.

In a production version, the AI call would replace the `pickRoute()` 
function entirely — the rest of the app stays identical. The architecture 
is already set up for this.

---

## 🗺️ Routes

### Route 1 — Mustamäe tee 149 → Bolt HQ
*Triggered when input contains "mustamäe" or "mustamae" AND "bolt", "hq", 
or "vana"*

| Leg | Mode | From | To | Time | Cost |
|-----|------|------|----|------|------|
| 1 | 🛴 Bolt Scooter | Mustamäe tee 149 | Järve tram stop | 5 min | €1.20 |
| 2 | 🚌 Tram Line 3 | Järve | Ülemiste | 14 min | €1.00 |
| 3 | 🚗 Bolt Ride | Ülemiste stop | Bolt HQ, Vana-Lõuna 15 | 7 min | €3.80 |
| | **Total** | | | **26 min** | **€6.00** |

### Route 2 — Default (any other input)
*Triggered for all other location combinations*

| Leg | Mode | From | To | Time | Cost |
|-----|------|------|----|------|------|
| 1 | 🛴 Bolt Scooter | Viru Keskus | Hobujaama tram stop | 7 min | €1.50 |
| 2 | 🚌 Tram Line 2 | Hobujaama | Ülemiste | 12 min | €1.00 |
| 3 | 🚗 Bolt Ride | Ülemiste stop | Ülemiste City | 5 min | €3.20 |
| | **Total** | | | **24 min** | **€5.70** |

---

## 🔮 What I'd Improve Next

- Connect a real AI API for dynamic route generation for any address 
  in Tallinn
- Integrate real-time public transport data from Tallinn's open 
  GTFS feed
- Add departure time input so routes adjust based on live 
  tram schedules
- Add a map view showing the route visually
- Expand beyond Tallinn to other Bolt cities
- AI re-routing — if your tram is delayed, automatically suggest 
  the next best option

---

## 📁 Project Structure

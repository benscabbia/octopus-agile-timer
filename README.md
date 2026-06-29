# ⚡ Agile Timer

A single self-contained web page that tells you the cheapest times to run your
**washing machine**, **dishwasher**, and **air conditioner** on the Octopus Energy
**Agile** tariff — so you don't have to squint at the half-hourly prices in the app every night.

- **No server, no build, no login, no dependencies.** Just one `index.html`.
- Fetches live prices straight from the public Octopus API in your browser.
- Works on a laptop and as a phone home-screen bookmark.

**▶ Live app:** https://benscabbia.github.io/octopus-agile-timer/

Defaults to region **A**. Pick your region in Settings (dropdown A–P, or postcode lookup).

---

## What it shows

**At a glance** — a compact table right at the top with the single best time for each
appliance, so you can eyeball it in a second. Scroll down for the full detail.

**Washing machine & dishwasher** — each gets two recommendations:

| Recommendation | What it means |
| --- | --- |
| **Best overnight (by deadline)** | Cheapest start so the cycle finishes by **07:00 on weekdays / 08:00 at weekends**. Ranked by lowest *average* p/kWh over the whole run, with the first-slot (peak-power) price shown and flagged ⚠ if it's unusually pricey. Plus a few alternative start times. |
| **Extra run today (finish by a latest time)** | For ad-hoc daytime loads — the cheapest start that still **finishes by your latest-finish time (22:00 by default)**. Only shown during your active hours (07:00–19:00), since that's when you'd actually start one. Includes a "soonest possible" option. |

**Air conditioner** — auto-detects the kind of day:

- **Price bands:** aircon prices carry a 💡 band — **cheap** (<20 p/kWh), **amber** (20–30), **bit pricey** (30–40), **expensive** (40+) — shown in the card and the at-a-glance table.
- **Normal day:** "Run 19:00–22:00" (your usual set-and-forget).
- **Expensive day — switch on early or wait?** A **binary** choice: switch on up to an hour early (default 21:00) **or** wait for the trigger (22:00). It treats the whole early hour as one block (its **average**), since 30-min steps barely differ. It goes early only if that hour is **not pricey** (avg under 30 p/kWh) **and not much dearer than the trigger price** (within a margin, default 8 p/kWh); otherwise it says wait. The card shows both options — early-hour average vs the trigger price — band-coloured.

**Price curve** — a colour-coded chart (green = cheap → red = expensive, blue = negative) with your recommended windows highlighted and a "now" marker.

**Availability banner** — tells you when tomorrow's prices aren't out yet
("check back after ~4pm") so you know to look again later; the *extra run now*
suggestions keep working regardless.

---

## Using it

1. Open `index.html` in any modern browser (double-click it, or host it — see below).
2. It loads today's + tomorrow's prices automatically and shows the recommendations.
3. Tap **↻ Refresh** any time (e.g. after 4pm when tomorrow's prices land).
4. Open **⚙︎ Settings** to tweak anything — it's all saved in your browser (`localStorage`).

### Settings you can change
- **Region** — dropdown (A–P) or type your **postcode** and tap *Find region*.
- **Run durations** — washer 2.5 h, dishwasher 3.5 h by default.
- **kWh per cycle** *(optional)* — fill these in to also see an estimated **£/run**.
- **Finish-by times** — 07:00 weekday / 08:00 weekend.
- **Extra run must finish by** — latest-finish time for daytime extra loads (default 22:00).
- **Extra-run active hours** — when an extra-run suggestion is shown (default 07:00–19:00).
- **Start granularity** — on the hour (matches most appliance delay timers) or every 30 min.
- **Aircon** — evening start + **latest time to trigger** (the run window; its end is the latest you'd switch on for the night), **how many hours early** you'd consider switching on (default 1) and the **"wait if dearer than trigger by" margin** (default 8 p/kWh),
  the **"pricey" threshold** (p/kWh above which the run is tagged pricey; default 25),
  and the "expensive day" thresholds (peak ≥ ×median, or peak ≥ an absolute p/kWh).

---

## Add it to a phone home screen

1. Open the hosted URL in your phone browser.
2. **iOS (Safari):** Share → **Add to Home Screen**. **Android (Chrome):** menu → **Add to Home screen**.
3. You get an "Agile Timer" icon that opens full-screen like an app.

> Settings are stored per-browser, so set your preferences once on each device.

## Hosting (optional)

The page is a single static file, so host it however you like:

- **Just open it** — double-click `index.html`, or email it to yourself / put it in
  cloud storage and open in your phone browser.
- **Static host** — drop it on any static web host (e.g. GitHub Pages, Netlify,
  Cloudflare Pages) or any web server on your network for a stable URL.

No backend or database is needed — the page does everything client-side, and the
Octopus pricing API allows cross-origin browser requests (`Access-Control-Allow-Origin: *`).

---

## Notes & accuracy

- Prices shown are **inc. VAT, in p/kWh**, in **Europe/London** time (BST/GMT handled automatically).
- "Best" ranks by the **average** price across the whole run; exact appliance
  power profiles aren't modelled, so treat the start-slot flag as a sanity check.
- Aircon advice is **guidance only** — how long cooling lasts depends on your room.
- Tariff/product code defaults to `AGILE-24-10-01`. If Octopus moves you to a newer
  Agile product and prices stop loading, update **Agile product code** in Settings.

*Data from the public Octopus Energy API. For guidance only — not financial advice.*

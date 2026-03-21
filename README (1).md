# Sports Countdown Widget

A live, embeddable sports countdown widget built for my UX/Product Design portfolio. It displays real-time countdowns to the next scheduled game for four of my favorite teams — pulling live data from ESPN's public API with no backend, no database, and no API keys required.

**[View it live on my portfolio →](#)** *(replace with your Framer URL)*

---

## What It Does

Four team cards sit side by side in a 2×2 grid. Each card shows one of three states:

- **Upcoming game** — a live countdown timer (days, hours, minutes, seconds) to the next scheduled game, along with the opponent and game date
- **Game in progress** — a "Live" badge with either the current score (Arsenal) or an "In Progress" indicator with the current period or half (Sharks, 49ers, Giants)
- **Offseason** — a clean "Offseason" state when no upcoming games are scheduled

The widget fetches fresh schedule data on every page load and updates the countdown every second.

**Teams covered:**
| Team | League | ESPN ID |
|------|--------|---------|
| San Jose Sharks | NHL | 18 |
| Arsenal FC | Premier League | 359 |
| San Francisco 49ers | NFL | 25 |
| SF Giants | MLB | 26 |

---

## Why I Built This

I wanted to add something personal to my portfolio that went beyond case studies — something that showed who I am outside of work. As a Bay Area sports fan and Arsenal supporter, a live game countdown felt like the right fit.

It also became a real design and product challenge in its own right:

- **Hierarchy and consistency** — making sure the countdown, live, and offseason states all felt like they belonged to the same design system, with aligned typography and spacing
- **Accessibility** — auditing contrast ratios across all four card colors and making intentional decisions about readability vs. brand color
- **Graceful degradation** — handling edge cases like offseason states, live games with unavailable scores, cross-year league schedules, and API inconsistencies
- **Responsive design** — the 2×2 grid collapses to a single column on mobile

---

## Technical Overview

The entire widget is a single self-contained HTML file — no frameworks, no build tools, no dependencies beyond Google Fonts.

**How it works:**

1. On page load, JavaScript fires requests to ESPN's public API for each team's schedule
2. The code first checks if any game is currently in progress using ESPN's `status.type.state` field
3. If a live game is found, the card shows a live state — with score if available, or "In Progress" with period detail if not
4. If no live game is found, it filters for the next future game and starts a countdown
5. If no future games exist at all, the card falls back to the offseason state

**A few interesting problems solved along the way:**

- ESPN's API returns scores in inconsistent formats depending on sport and game state — sometimes a plain string, sometimes a nested object. A small helper function normalizes both cases
- The Premier League season runs August–May, crossing two calendar years. ESPN's team schedule endpoint only returns one calendar year at a time, so Arsenal's data is fetched via a date-range scoreboard endpoint instead, covering the full season in two queries
- For NHL, NFL, and MLB, both regular season (`seasontype=2`) and postseason (`seasontype=3`) are fetched and merged so playoff games are always included
- NHL, NFL, and MLB schedule endpoints don't include live scores during in-progress games — the widget detects this and shows "In Progress" with the period detail instead of a broken score
- ESPN team IDs are not always intuitive and using a wrong ID causes the widget to silently show the wrong team's data — IDs were verified by fetching the full team list directly from the ESPN API

---

## Files

| File | Description |
|------|-------------|
| `sports-countdown.html` | The complete widget — HTML, CSS, and JavaScript in one file |
| `sports-widget-docs.docx` | Full product and technical documentation |

---

## Embedding

The widget is embedded in Framer as a native HTML Code Embed component. Paste the contents of `sports-countdown.html` into a Framer Code Embed, set the width to match your content column, and set the height to ~520px on desktop and ~900px on mobile.

The widget runs entirely client-side. All ESPN API calls happen in the browser — no server needed.

---

## Annual Maintenance

The only piece that requires manual updates is Arsenal's date range parameters, which are hardcoded for the 2025–26 EPL season. At the start of each new season (typically August), update the two date ranges in the `getSoccerUrls` function to cover the new season's dates.

---

## About

I'm a UX/Product Designer based in the Bay Area. This project is part of my portfolio — built to demonstrate that I'm comfortable working across design and code, and that I bring a point of view to everything I make.

**[Portfolio](#)** · **[LinkedIn](#)** *(replace with your links)*

# Sports Countdown Widget

A live, embeddable sports countdown widget built for my UX/Product Design portfolio. It displays real-time countdowns to the next scheduled game for four of my favorite teams — pulling live data from ESPN's public API with no backend, no database, and no API keys required.

**[View it live on my portfolio's About page →](https://cparmar.framer.website/about)** 

---

## What It Does

Four team cards sit side by side in a 2×2 grid. Each card shows:

- **Active season** — a live countdown timer (days, hours, minutes, seconds) to the next scheduled game, along with the opponent and game date
- **Offseason** — a clean "Offseason" state when no upcoming games are scheduled

The widget updates every second and fetches fresh schedule data on every page load.

**Teams covered:**
| Team | League |
|------|--------|
| San Jose Sharks | NHL |
| Arsenal FC | Premier League |
| San Francisco 49ers | NFL |
| SF Giants | MLB |

---

## Why I Built This

I wanted to add something personal to my portfolio that went beyond case studies — something that showed who I am outside of work. As a Bay Area sports fan and Arsenal supporter, a live game countdown felt like the right fit.

It also became a real design and product challenge in its own right:

- **Hierarchy and consistency** — making sure the active (countdown) and inactive (offseason) states felt like they belonged to the same design system, with aligned typography and spacing
- **Accessibility** — auditing contrast ratios across all four card colors and making intentional decisions about readability vs. brand color
- **Graceful degradation** — handling edge cases like offseason states, cross-year league schedules (the EPL season straddles two calendar years), and API inconsistencies
- **Responsive design** — the 2×2 grid collapses to a single column on mobile

---

## Technical Overview

The entire widget is a single self-contained HTML file — no frameworks, no build tools, no dependencies beyond Google Fonts.

**How it works:**

1. On page load, JavaScript fires requests to ESPN's public API for each team's schedule
2. The code filters for upcoming games, sorts by date, and finds the next scheduled game
3. The countdown is calculated from the current time and ticks every second via `setInterval`
4. If no upcoming games are found, the card falls back to an offseason state

**A few interesting problems solved along the way:**

- ESPN's API returns scores in inconsistent formats depending on sport and game state — sometimes a plain string, sometimes a nested object. A small helper function normalizes both cases
- The Premier League season runs August–May, crossing two calendar years. ESPN's team schedule endpoint only returns one calendar year at a time, so Arsenal's data is fetched via a date-range scoreboard endpoint instead, covering the full season in two queries
- For NHL, NFL, and MLB, both regular season (`seasontype=2`) and postseason (`seasontype=3`) are fetched and merged so playoff games are always included

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

**[Portfolio](https://cparmar.framer.website/)** · **[LinkedIn](https://www.linkedin.com/in/ckparmar80/)**

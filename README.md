# Zabawa Aktywnościowa 2026 — Team Fitness Challenge Tracker

A self-contained web app for running a weekly team fitness challenge between two teams. Built as a single HTML file with no build step, optional cloud sync, and a polished read-only export for participants.

## What is `tabela.html`?

`tabela.html` is the **admin dashboard** — the single file where activities are entered, points are calculated, and weekly results are generated. It's designed to be opened in a browser (desktop or mobile) and used by one or two trusted administrators to log everyone's weekly workouts.

It is **not** a participant-facing page. Participants receive a separate, read-only HTML report generated from this tool (see "Exporting results" below).

## Core features

### Scoring engine
- Points for running (5 pts/km, 3 km minimum, max 2 runs/day)
- Points for walking, cycling, and swimming, converted to "running-equivalent" km via multipliers (walk ×0.5 with 3 km minimum, bike ×0.2, swim ×5.0)
- Points for timed activities (gym, yoga, pilates, etc.) based on duration tiers, capped at 4 scored sessions per week
- Daily activity bonus (+20 pts, once per active day regardless of how many activities)
- Weekly regularity bonus (based on number of active days, capped at 5+ days)
- Weekly running bonus (based on number of running days)
- Team-wide daily participation bonus (based on % of team active that day)
- Individual contribution cap (dynamic, based on team size: 200% / team size)

### Team management
- Add or remove participants on the fly — team rosters are stored in the data file, not hardcoded
- Customize team names, logos, and mascots (emoji or uploaded images)
- Set a challenge start date so weekly numbering and date ranges are calculated automatically

### Week management
- **Close Week**: freeze a week's final results (including historical roster, even if members have since been removed) into a permanent record
- **Start New Week**: clear daily activity entries for the next week while preserving the cumulative season score

### Data persistence (three options, can be combined)
1. **Local browser storage** — always-on fallback, works offline
2. **File System Access API** — save/load a `tabela_dane.json` file directly (Chrome/Edge desktop)
3. **Supabase cloud sync** — optional real-time sync between two logged-in admins, so both can edit from different devices without conflicts

### Exporting results
- **HTML export** (`wyniki_DDMMYYYY_XX.html`): a standalone, offline-capable report for participants, with four tabs:
  - **Results** — team scores, per-player breakdowns with expandable daily activity details
  - **Statistics** — rankings by points, distance, active days, and best single day
  - **Chronicle** — a generated weekly narrative plus a day-by-day team race visualization
  - **Achievements** — weekly awards (MVP, top runner, most consistent, etc.) per team
- **CSV export**: full weekly data table for spreadsheet analysis
- **JSON backups**: timestamped, versioned snapshots (`backup_DDMMYYYY_vN.json`) for safekeeping

## Tech stack

- Plain HTML, CSS, and vanilla JavaScript — no build tools, no frameworks
- Optional [Supabase](https://supabase.com) integration for auth and real-time sync (free tier is more than sufficient)
- Can be hosted for free on GitHub Pages

## Getting started

1. Open `tabela.html` in a browser
2. Choose a starting option: load an existing data file, continue from browser storage, or start fresh
3. Click on a team member to log their activities for the week
4. Use the menu (☰) to export results, manage the roster, close/start weeks, and configure settings

For cloud sync setup (optional), see `TUTORIAL_SUPABASE.md`.

## Project files

| File | Purpose |
|---|---|
| `tabela.html` | Admin dashboard (this app) |
| `regulamin.html` | Full rules (Polish) |
| `sciagawka-punkty.html` | Quick scoring reference card |
| `kalkulator.html` | Standalone weekly points calculator |
| `druzyny.html` | Read-only team roster page |
| `przewodnik.html` | Plain-language FAQ for participants |
| `PAMIEC_PROJEKTU.md` | Project memory / technical documentation |
| `TUTORIAL_SUPABASE.md` | Step-by-step cloud sync setup guide |

## Language note

The UI, rules, and participant-facing content are in **Polish**, as this was built for a Polish-speaking WhatsApp group. Code comments and this README are in English for broader accessibility.

## License

Personal project — no formal license. Feel free to adapt for your own group challenge.

# Pulse — Employee Attendance & Clock-In

A single-file attendance board for G9 Outsourcing / NYTelecon. Agents clock in from a
browser; supervisors see who is in, late, MIA, absent or on leave, and whether each
campaign has the headcount it was promised.

Everything is in **`index.html`**. No build step, no server, no dependencies.

## Put it on GitHub Pages

1. Create a new repository on GitHub (public).
2. Upload `index.html` to the top level of the repo. Keep the name `index.html`.
3. Go to **Settings → Pages**.
4. Under *Build and deployment*, set **Source** to `Deploy from a branch`,
   **Branch** to `main` and the folder to `/ (root)`. Save.
5. Wait about a minute. Your app is live at
   `https://<your-username>.github.io/<repo-name>/`

To update it later, edit `index.html` in GitHub and commit — Pages redeploys itself.

## Signing in

Any email address and any password are accepted. The buttons on the sign-in screen
jump straight to a role:

| Sign-in | Sees |
|---|---|
| Abi Esmao | the agent view — today's schedule and the clock-in button |
| Cha / Jovi | Team Leader — live board, coverage, their own segments |
| Tessa Jacob | Admin — everything, plus CSV exports |

Try it in this order: sign in as **Abi**, clock in, sign out, sign back in as
**Tessa**, and watch Abi's row on the live board change.

## What's in it

- **Agent view** — today's schedule with each shift segment and its owning TL, one
  big clock-in button, break tracking, a live shift timer, and a week view.
- **Live board** — status counters (Clocked In / Late / MIA / Absent / On Leave /
  Rest Day / Not Yet Due), a per-agent table with a TL-coloured segment ribbon, and
  a "needs attention" list.
- **Coverage vs requirement** — required FTE against who is actually clocked in right
  now, per campaign, worst shortfall first, with live Required / Available / Balance
  roll-ups that replace the broken `#REF!` rows in the spreadsheet.
- **Reports** — CSV export of the daily attendance register, coverage, and exceptions.
- Dark mode, keyboard accessible, works on a phone.

## Important limits

This is a **front-end prototype**, not a production system:

- **Data lives in the visitor's own browser** (`localStorage`). It is not shared
  between people or devices, and clearing browser data erases it. Two supervisors
  opening the link will *not* see each other's clock-ins.
- **The sign-in is not real security.** Any email and password get in. Do not put
  real personal data in this version.
- Schedules are **generated** from the roster so the demo always has something to
  show. They are stable for a given day, but they are not your real schedule.

When you want shared, permanent data and real logins, this file becomes the front end
and you add a backend behind it — `ClockIn_App_Build_Prompt.md` in the same project
folder is the full specification for that build.

## Making it yours

Open `index.html` and edit the lists near the top of the `<script>` block:

- `REGION_WINDOW` — shift windows per region (AU, SEA, MEA, EU, NA)
- `CAMPAIGNS` — campaign name, client, type, region, owning TL
- `REQUIRED` — required FTE per campaign per day
- `AGENTS` — the roster
- `TL_COLOR` — the colour each TL gets in the segment ribbon
- `SETTINGS` — grace period, MIA threshold, auto-absent threshold

Save, re-upload, done.

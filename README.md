# Deep Research: MBA Trimester II Speaking Practice

A single-page website for practising speaking. Spin a topic, research it on a timer, then speak on it.
Topics come only from the five Trimester II course plans (Sep-Dec 2026, batch 2026-28).

## Run it
No build step. Double-click `index.html`, or serve the folder with any static host
(`npx serve .`, Netlify Drop, GitHub Pages). Fonts load from Google Fonts and fall back to system fonts offline.

## Folder map
- `index.html`: the whole site (HTML + CSS + JS + topic data in one file)
- `data/topics.json`: a readable copy of all topics, grouped by course and unit. It is for reference/editing only; the site reads the `S` object inside `index.html`, so copy changes back there (or wire the page to fetch this JSON).
- `HOW_TO_PLAY.md`: rules text written for users (could be added to the site as a "How to play" section)
- `reference/unprompted-screenshot.png`: the design the look is modelled on
- `reference/course-plans/`: the five uploaded course plans (MBA231 AMM docx; MBA232 MHR, MBA234 FM, MBA235 OM, MBA236 BAAI PDFs)

## How the page works (in `index.html`)
- `S` = topic data: `S.KEY.n` (course name) and `S.KEY.u` = list of `[unit label, [ "question|angle1;angle2;angle3", ... ]]`. Courses: AMM, MHR, FM, BAAI, OM.
- State: `sel` (subject or "ALL"), `rM` research minutes (default 5), `sM` speech minutes (default 2), `cur` (current topic), `notes`.
- Flow functions: `idle()` -> `spin()` -> `showTopic()` -> `research()` -> `speak()` -> `finish()`.
- `run(secs, done)` drives the countdown; `beep()` plays the end tone; Space triggers the main button (`#pri`).
- Settings chips: research options `[2,3,5,10]`, speech options `[1,2,3,5]` (see `drawTimes` calls at the bottom).

## Design tokens (top of the `<style>` block)
Dark warm gradient (brown top-left, teal top-right, navy bottom), cream text `--ink`, terracotta accent `--acc`,
Playfair Display for big text, Outfit for UI. A light-mode variant is defined under `prefers-color-scheme: light`.
Topic text size auto-shrinks by length (`sz()` -> classes xl / lg / md / sm).

## Add or edit topics
Add a string inside a unit's array in `S`: `"Your speakable question?|angle one; angle two; angle three"`.
Avoid the `|` and `;` characters inside the question or angles.

## Known limits / ideas to build next
- Notes are not saved (no storage). Could add localStorage when hosted on your own site.
- No voice recording or feedback yet.
- Topics are about 60 questions; more per unit, difficulty levels, or exam-style questions could be added.
- Add a "How to play" section from `HOW_TO_PLAY.md`.
- Optional: split CSS/JS/data into separate files and load `data/topics.json` with `fetch`.

## Credits
Layout and feel inspired by the Unprompted speaking-practice site (screenshot in `reference/`). Branding was not copied.

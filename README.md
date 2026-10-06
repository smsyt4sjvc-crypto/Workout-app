# EXM‑3700LP Workout Log

A one‑page, offline‑capable set logger for the **Body‑Solid EXM‑3700LP** home gym (plus the GKR9 knee‑raise / dip attachment). No accounts, no server: everything is stored on the phone until you press **Reset**, and **Copy** puts the whole log on the clipboard so you can paste it here or into a notes app.

## Use it

1. Open the app: **https://smsyt4sjvc-crypto.github.io/Workout-app/**
   (needs GitHub Pages turned on once — see below).
2. Add it to your home screen:
   - **iPhone / iPad (Safari):** Share → *Add to Home Screen*.
   - **Android (Chrome):** ⋮ menu → *Add to Home screen* / *Install app*.
3. Set your name with the picker at the top right (it also asks the first time you copy).
4. In the gym: pick the exercise, set **Plates** and **Reps**, tap **Log set**. Each tap records one set with today's date. Tap **×** on a set to remove it. The card shows today's sets and what you did last session. Tap the picture (or **How to ›**) for a larger photo and the numbered steps.
5. Afterwards: **Copy all** (or **Copy today**) and paste it into the chat with Claude to be saved to your file in [`logs/`](logs/), or into your notes.
6. **Reset** wipes the logged sets and plate/rep selections of whoever is selected. It asks first.

## Routines

Load a plan and the app shows each day's exercises in order, with targets, setup notes and progress (e.g. "2 of 3 sets ✓"). Tap **Load routine** (or **Edit**) at the top, paste the routine and **Save**. The app opens on today's weekday; tap another day to see it. Each person has their own routine, and **Reset** leaves it in place.

A routine is plain text, one line per exercise:

```
EXM-3700LP routine · Weekly plan

## Mon · Full Body A
Warm-up: bike easy 5 min
A1 Leg Press: 3 × 8–12 | Back pad set so knees are at 90°
A2 Calf Press: 3 × 12–15
B1 DB Single-Arm Row: 3 × 10–12/arm | Free hand braced on the seat pad
B2 Plank: 3 × 30–45 sec
Cardio: Bike sprints, 10 min
```

- `## Day · title` starts a day. Lines sharing a letter (A1, A2…) are a superset or circuit.
- `/arm`, `/leg` or `/side` means each side. `sec` makes it a timed hold, logged in seconds.
- Machine exercises use the app's names and log plates. Names starting `DB ` log pounds (0 = bodyweight), `Band ` logs Light / Medium / Heavy, anything else is bodyweight reps. Add `(DB)` or `(band)` after a name to override.
- `Warm-up:`, `Cardio:`, `Cool-down:` and `Note:` lines show as notes. Notes before the first day go under *Plan notes*.
- The routine sheet lists any line it couldn't read, and **Copy instructions for Claude** copies a prompt that gets any Claude chat to write a routine in this format.

[`routines/weekly-plan.txt`](routines/weekly-plan.txt) is the weekly G9S plan in this format.

## More than one person

Everyone uses the same app and link; each person's sets are kept apart.

- **On their own phone** (simplest): they add the app to their home screen and set their name. Phones never share data.
- **Sharing one phone:** use the name picker → *Add a person…*, then switch between names. Each name has its own sets, plate/rep settings and Reset. *Remove …* deletes that person's log from the phone.
- **In the repo:** one file per person in `logs/`, named after the name at the top of the copied log (`· Sam` → `logs/sam.md`). All on `main`. No branches, because GitHub Pages serves a single branch and the app is the same for everyone.

## Exercises

Grouped as on the Body‑Solid exercise chart. The photo and the numbered steps for each come from the Body‑Solid G9S chart (`img/*.jpg`), which has the same stations as the EXM‑3700LP; the three marked * are not on the chart, so they carry standard form cues and a drawing from the owner's manual instead.

| Group | Exercises |
| --- | --- |
| Chest | Chest Press · Incline Press · Pectoral Fly |
| Shoulders | Standing Shoulder Press · Upright Row · Lateral Deltoid Raise |
| Back | Lat Pull Down · Back Hyperextension · Chest Supported Mid Row · Seated Row * |
| Arms | Biceps Curl · Triceps Press Down · Triceps Extension |
| Abs | Resistance Ab Crunch · Oblique Crunch · Oblique Bend |
| Hips / Thighs | Leg Abduction · Glute Kickback · Leg Press (2:1) |
| Legs | Leg Extension · Standing Leg Curl · Calf Press (2:1) |
| GKR9 (bodyweight) | Vertical Knee Raise * · Dips * |

Each stack is 210 lb in 10 lb plates (max 21). The leg press runs a 2:1 ratio, so the app shows both the stack weight and the pressed weight. To change exercises, steps or plate weight, edit `GROUPS`, `PLATE_LB` and `MAX_PLATES` near the top of the script in `index.html`.

## Copied log format

```
EXM-3700LP workout log · Sam
Exported 2026-10-06 18:02 · 5 sets

2026-10-06 Tue
- Chest Press: 8 plates / 80 lb × 12, 10 | 9 plates / 90 lb × 8
- Leg Press: 12 plates / 120 lb stack · 240 lb press × 15
- Dips: bodyweight × 12
```

The first line names whose log it is. Sets are listed in the order you logged them; consecutive sets at the same weight share one `×` list. Routine exercises read like `- DB Single-Arm Row (each arm): 12.5 lb × 10, 10, 10`, `- Band Face Pull: medium band × 15` and `- Plank: 45 s, 40 s`.

## Where the data lives

In the browser's `localStorage` for this site, on that device only, with a separate slot per person (`exm3700lp.people` lists the names). It survives closing the app and restarting the phone, but **clearing Safari/Chrome site data deletes it**, so copy the log out regularly. The service worker caches the page so it opens with no signal.

## Turning on GitHub Pages (one time)

Repo **Settings → Pages → Build and deployment → Source: "Deploy from a branch" → Branch: `main`, folder `/ (root)` → Save**. The site goes live at the URL above within a minute or two.

## Files

- `index.html` — the whole app (HTML, CSS, JS; no dependencies)
- `img/` — one photo per exercise from the Body‑Solid chart, plus two drawings from the manual
- `manifest.webmanifest`, `sw.js`, `icons/` — home‑screen install and offline cache (photos included)
- `logs/` — one saved log per person (`logs/<name>.md`)
- `routines/` — routines ready to paste into the app

# EXM‑3700LP Workout Log

A one‑page, offline‑capable set logger for the **Body‑Solid EXM‑3700LP** home gym (plus the GKR9 knee‑raise / dip attachment). No accounts, no server: everything is stored on the phone until you press **Reset**, and **Copy** puts the whole log on the clipboard so you can paste it here or into a notes app.

## Use it

1. Open the app: **https://smsyt4sjvc-crypto.github.io/Workout-app/**
   (needs GitHub Pages turned on once — see below).
2. Add it to your home screen:
   - **iPhone / iPad (Safari):** Share → *Add to Home Screen*.
   - **Android (Chrome):** ⋮ menu → *Add to Home screen* / *Install app*.
3. In the gym: pick the exercise, set **Plates** and **Reps**, tap **Log set**. Each tap records one set with today's date. Tap **×** on a set to remove it. The card shows today's sets and what you did last session. Tap the picture (or **How to ›**) for a larger photo and the numbered steps.
4. Afterwards: **Copy all** (or **Copy today**) and paste into [`LOG.md`](LOG.md) or your notes.
5. **Reset** wipes every logged set and your plate/rep selections. It asks first.

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
EXM-3700LP workout log
Exported 2026-10-06 18:02 · 5 sets

2026-10-06 Mon
- Bench Press: 8 plates / 80 lb × 12, 10 | 9 plates / 90 lb × 8
- Leg Press: 12 plates / 120 lb stack · 240 lb press × 15
- Dips: bodyweight × 12
```

Sets are listed in the order you logged them; consecutive sets at the same weight share one `×` list.

## Where the data lives

In the browser's `localStorage` for this site, on that device only. It survives closing the app and restarting the phone, but **clearing Safari/Chrome site data deletes it**, so copy the log out regularly. The service worker caches the page so it opens with no signal.

## Turning on GitHub Pages (one time)

Repo **Settings → Pages → Build and deployment → Source: "Deploy from a branch" → Branch: `main`, folder `/ (root)` → Save**. The site goes live at the URL above within a minute or two.

## Files

- `index.html` — the whole app (HTML, CSS, JS; no dependencies)
- `img/` — one photo per exercise from the Body‑Solid chart, plus two drawings from the manual
- `manifest.webmanifest`, `sw.js`, `icons/` — home‑screen install and offline cache (photos included)
- `LOG.md` — paste copied logs here to track them in the repo

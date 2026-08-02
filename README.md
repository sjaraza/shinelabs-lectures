# ShineLabs Robotics — lecture decks

Slides for a four-part volunteer robotics series for high-school students,
built around SunFounder PiCar-X kits on Raspberry Pi Zero 2 W.

Open `index.html` in a browser. No build step, no internet needed.

| | | |
|---|---|---|
| **Lecture 0** | Getting to Know Your Robot | hardware, network, SSH, dashboard, drive, camera |
| **Lecture 1** | Sensors and Decisions | sensors → decisions, basic CV, efficient wheeled control |
| **Lecture 2** | Seeing | image processing and CV fundamentals, a touch of ROS |
| **Lecture 3** | Autonomy | intro to SLAM with ultrasonic and camera |

Only lecture 0 exists so far.

## Design constraints

These aren't arbitrary — each one comes from the room the slides are used in.

**Fully offline.** reveal.js 6.0.1 is vendored in `vendor/reveal.js` (dist and
plugins only). No CDN links, no web fonts. A classroom's internet cannot be
relied on, and the one uplink present is shared with 20 robots.

**Interactive, not presented.** Each session is 90 minutes and is mostly
hands-on. The slides carry the commands students type, set large enough to read
from the back of the room, and every hands-on segment ends in a **checkpoint** —
a single visible thing everyone should be able to point at, so the room can be
scanned at a glance.

**No credentials in the repo.** This repo is public. Wi-Fi passwords go on the
board, not on a slide. There are no student names or photographs of minors.

**Placeholders are loud.** Unfilled artwork and TODO commands render as dashed
amber boxes, so a gap is obvious in rehearsal rather than on the day.

## Layout

```
index.html              landing page linking the four decks
assets/theme.css        classroom projector theme over reveal.js black
assets/*.png            photos, screenshots, QR codes  (to be added)
lecture-0/index.html    the deck
lecture-0/NOTES.md      run of show, pre-flight checklist, failure modes
vendor/reveal.js/       reveal.js 6.0.1, offline
```

`lecture-0/NOTES.md` is the useful file if you are actually delivering the
session: minute-by-minute timings, a pre-flight checklist, the list of
outstanding placeholders, and a table of things that will go wrong with the
answer to each.

## Presenting

- `S` — speaker notes in a second window; every slide has them
- `Esc` — slide overview · `F` — fullscreen · `B` — blank the screen
- Arrow keys — left/right between segments, up/down within a segment

Print to PDF via `?print-pdf` appended to the deck URL, then the browser's print
dialogue.

## Related

The student-side robot dashboard and the Pi provisioning script live in
[`shinelabs-robot-dashboard`](https://github.com/sjaraza/shinelabs-robot-dashboard).

## Licence

Slide content © the author. reveal.js in `vendor/` is MIT, see
`vendor/reveal.js/LICENSE`.

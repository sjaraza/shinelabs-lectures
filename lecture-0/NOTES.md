# Lecture 0 — run of show

90 minutes, 20 students, one robot and one laptop each. Deliberately
hands-on: the slides are a spine, not the content.

| Time | Segment | Mode | Ends with |
|---|---|---|---|
| 0:00–0:08 | Welcome, intro, series arc, Slack | slides | everyone in Slack |
| 0:08–0:20 | Meet the hardware | robot in hand | can point at each part |
| 0:20–0:28 | Network + imaging demo | projector only | — |
| 0:28–0:45 | First contact: power on, SSH in | hands-on | **Checkpoint 1** — prompt says `ali@robotN` |
| 0:45–0:55 | Run the setup script | hands-on | **Checkpoint 2** — script prints `READY` |
| 0:55–1:02 | Dashboard: clone, run, connect | hands-on | **Checkpoint 3** — battery + distance live |
| 1:02–1:12 | Drive it | hands-on, on the floor | **Checkpoint 4** — forward, turn, return, stop |
| 1:12–1:20 | Aim camera, capture | hands-on | **Checkpoint 5** — a photo on screen |
| 1:20–1:30 | Battery care, pack down, next time | slides | batteries collected |

Checkpoints exist so the room can be scanned at a glance. Don't move on until
most of the room is at the same place; park stragglers with a neighbour who is
already through.

## Before the session

- [ ] Router: **Smart Connect off**, separate SSIDs — robots on 2.4 GHz
      (`ShineLabs`), laptops on 5 GHz. A Pi Zero 2 W is 2.4 GHz only, and 40
      clients on one band will hurt.
- [ ] All 20 cards imaged, each with a **unique hostname** (`robot0`…`robot19`)
      so `robotN.local` resolves
- [ ] Every robot **physically labelled** with its hostname. Without this,
      twenty students spend ten minutes working out which robot is theirs.
- [ ] Batteries charged. Two LEDs lit on every pack before students arrive.
- [ ] Two or three spare charged packs within reach
- [ ] Gateway laptop up, `./scripts/status.sh` reports READY (see `slab-gw`)
- [ ] Wi-Fi passwords written on the board — **not** on a slide, since the deck
      is in a public repo
- [ ] Slack QR scans from the back of the room (test it on the projector, not
      just on screen)
- [ ] Rehearse once end-to-end on one robot; every placeholder filled

## Placeholders still to fill

| File / slide | What's needed |
|---|---|
| "Introduction" slide | instructor bio |
| `assets/robot-annotated.png` | annotated photo of the assembled PiCar-X |
| `assets/imager-customise.png` | screenshot of Imager's OS-customisation dialogue |
| `assets/dashboard.png` | screenshot of the finished dashboard |
| 5 GHz SSID | laptop network name |
| Setup script command | once the provisioning script exists |
| Clone + run commands | once the dashboard exists |

## Things that will go wrong, and the answer

| Symptom | Cause | Fix |
|---|---|---|
| `ping robotN.local` fails | robot not booted, or not on Wi-Fi | wait 40 s; check the HAT power switch |
| Robot boots then dies | flat pack | swap to a spare, hand the flat one in |
| SSH asks for a password students don't have | wrong user | it is `ali@`, not their own name |
| Servos twitch on first connect | `Picarx()` centres them on init | expected, not a fault |
| Robot pulls to one side when driving | uncalibrated | expected — it's lecture 1's opening problem |
| Distance reads `-1` | no echo returned | expected. This is the teaching moment, not a bug |
| Everything slow at once | 20 robots on one 2.4 GHz radio | split SSIDs beforehand |

## Deliberate omissions

- **How the network is built.** Not today's lesson, and it invites tangents.
  "There is a network, here's how you join" is enough.
- **Calibration.** Deferred to lecture 1, where a crooked-driving robot is a
  motivated problem rather than a chore. Also saves ~15 minutes here.
- **Live video.** A single still on demand instead — an honest trade-off on a
  512 MB board, and worth explaining as one.
- **Imaging as an activity.** Demoed only. Twenty students imaging cards live
  would consume the session.

## Presenting

- `S` opens speaker notes in a second window — every slide has them
- `Esc` for the slide overview, `F` for fullscreen
- Arrow keys: left/right moves between segments, up/down within a segment
- Works fully offline; reveal.js is vendored in `vendor/reveal.js`

## Repo notes (instructor)

Kept here rather than in the README, which students read.

- **Offline by design.** reveal.js 6.0.1 is vendored in `vendor/reveal.js`
  (`dist/` only — built plugins live at `dist/plugin/`, and the source `plugin/`
  tree was removed as it contains only TypeScript). No CDN links, no web fonts.
- **No credentials, ever.** This repo is public. Wi-Fi passwords go on the board.
  No student names, no photographs of minors.
- **Turn off Slack invites after lecture 0.** `assets/slack-qr.png` encodes a
  shared-invite URL, this repo is public, and a QR is trivially decodable — so
  the link is scrapeable for as long as it is live. Everyone who needs it will
  have joined in the first session. Slack → Manage members → invite links →
  revoke. Post-lecture-0 joiners can be invited by email instead.
- **Placeholders render as loud amber boxes** so an unfilled slot is obvious in
  rehearsal rather than on the day. Grep for `placeholder` to find them all.
- **Print to PDF** by appending `?print-pdf` to a deck URL, then print from the
  browser.

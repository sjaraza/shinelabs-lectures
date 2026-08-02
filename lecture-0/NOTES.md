# Lecture 0 — run of show

90 minutes, 20 students, one robot and one laptop each. Deliberately
hands-on: the slides are a spine, not the content.

Students image their own SD cards in this session, which is the single longest
segment. Timings below reflect that.

| Time | Segment | Mode | Ends with |
|---|---|---|---|
| 0:00–0:08 | Welcome, intro, series arc, Slack | slides | everyone in Slack |
| 0:08–0:18 | Meet the hardware — "how many sensors can you find?" | robot in hand | can point at each part |
| 0:18–0:24 | The robot network + label your robot | slides + stickers | every robot labelled |
| 0:24–0:50 | **Image the SD card** and boot | hands-on | **CP1** — `ping robotN.local` replies |
| 0:50–0:58 | SSH in | hands-on | **CP2** — prompt is `you@robotN` |
| 0:58–1:08 | Run the setup script | hands-on | **CP3** — script prints `READY` |
| 1:08–1:16 | Dashboard: clone, run, connect | hands-on | **CP4** — battery + distance live |
| 1:16–1:24 | Drive it | hands-on, on the floor | **CP5** — forward, turn, return, stop |
| 1:24–1:28 | Aim camera, capture | hands-on | **CP6** — a photo on screen |
| 1:28–1:30 | Battery care, pack down, next time | slides | batteries collected |

Checkpoints exist so the room can be scanned at a glance. Don't move on until
most of the room is at the same place; park stragglers with a neighbour who is
already through.

⚠️ **Imaging is the long pole and it will overrun for someone.** If you are past
1:20 and still fighting cards, cut CP5 and CP6 and open lecture 1 with driving —
what matters is that every robot is built, imaged and reachable. Do not cut the
battery-care slide.

## Before the session

**Materials — students image their own cards, so each student needs:**

- [ ] microSD card, **16 GB or larger**
- [ ] a **card reader** — many laptops have no SD slot, and this is the item
      most likely to be forgotten
- [ ] **Raspberry Pi Imager already installed** on their laptop. Ask them to do
      this before arriving: it is a ~150 MB download, and twenty of them at once
      over one uplink is a slow start to the session.
- [ ] a sticker and a marker, for labelling the robot
- [ ] 2–3 **spare pre-imaged cards** in your bag, for cards that fail or
      students who get hopelessly stuck

**Setup:**

- [ ] Router: **Smart Connect off**, separate SSIDs — robots on 2.4 GHz
      (`ShineLabs`), laptops on 5 GHz. A Pi Zero 2 W is 2.4 GHz only, and 40
      clients on one band will hurt.
- [ ] Robot numbers assigned per student — hand them out rather than letting
      students pick, or you will get two `robot0`s
- [ ] Batteries charged. Two LEDs lit on every pack before students arrive.
- [ ] Two or three spare charged packs within reach
- [ ] Gateway laptop up, `./scripts/status.sh` reports READY (see `slab-gw`)
- [ ] Wi-Fi name and password written on the board — **not** on a slide, since
      the deck is in a public repo. Students type these into Imager.
- [ ] Slack QR scans from the back of the room (test it on the projector, not
      just on screen)
- [ ] Rehearse once end-to-end on one robot; every placeholder filled

## Placeholders still to fill

| File / slide | What's needed |
|---|---|
| "Introduction" slide | instructor bio |
| `assets/dashboard.png` | screenshot of the finished dashboard |
| 5 GHz SSID | laptop network name |
| Setup script command | once the provisioning script exists |
| Clone + run commands | once the dashboard exists |

## Things that will go wrong, and the answer

| Symptom | Cause | Fix |
|---|---|---|
| Imager never showed a customisation step | they clicked SKIP CUSTOMISATION | rewrite the card — without it there is no hostname, no Wi-Fi and no SSH |
| `ping robotN.local` fails | wrong Wi-Fi details entered in Imager | check hostname spelling first, then rewrite the card |
| First boot seems to hang | filesystem expansion + Wi-Fi join | give it two minutes before declaring it broken |
| `ssh` asks for a password they don't know | they forgot what they typed in Imager | this is why the slide says write it down; otherwise rewrite the card |
| `ssh` refuses with a host-key warning | card rewritten, same hostname | on their laptop: `ssh-keygen -R robotN.local` |
| Two students both chose `robot0` | numbers not handed out | rename one: `sudo hostnamectl set-hostname robotN`, reboot |
| Robot boots then dies | flat pack | swap to a spare, hand the flat one in |
| Servos twitch on first connect | `Picarx()` centres them on init | expected, not a fault |
| Robot pulls to one side when driving | uncalibrated | expected — it's lecture 1's opening problem |
| Distance reads `-1` | no echo returned | expected. This is the teaching moment, not a bug |
| Everything slow at once | 20 robots on one 2.4 GHz radio | split SSIDs beforehand |

## Deliberate omissions

- **How the network is built.** Not today's lesson, and it invites tangents.
  "There is a network, here's how you join" is enough.
- **Calibration.** Deferred to lecture 1, where a crooked-driving robot is a
  motivated problem rather than a chore.
- **Live video.** A single still on demand instead — an honest trade-off on a
  512 MB board, and worth explaining as one.

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
- **`.nojekyll`** is present so GitHub Pages serves the tree verbatim rather than
  running it through Jekyll.
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

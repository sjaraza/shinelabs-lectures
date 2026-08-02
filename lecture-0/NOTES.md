# Lecture 0 — run of show

90 minutes, 20 students, one robot and one laptop each. Deliberately
hands-on: the slides are a spine, not the content.

Students image their SD card **at home, before the session**. The deck carries
the full instructions plus a QR anyway, as a catch-up path for anyone who
didn't — that is what the 0:24 block is for.

| Time | Segment | Mode | Ends with |
|---|---|---|---|
| 0:00–0:08 | Welcome, intro, series arc, Slack | slides | everyone in Slack |
| 0:08–0:18 | Meet the hardware — "how many sensors can you find?" | robot in hand | can point at each part |
| 0:18–0:24 | The robot network + label your robot | slides + stickers | every robot labelled |
| 0:24–0:34 | Imaging **catch-up** + boot | hands-on | **CP1** — `ping <name>.local` replies |
| 0:34–0:40 | Terminal + SSH client on the laptop | hands-on | `ssh -V` prints a version |
| 0:40–0:48 | SSH in | hands-on | **CP2** — prompt is `you@<name>` |
| 0:48–0:58 | Run the setup script | hands-on | **CP3** — script prints `READY` |
| 0:58–1:03 | `robot_play.py` — make it move from the robot | hands-on | a robot that moved, and someone who found the `-1` |
| 1:03–1:11 | Dashboard: clone, run, connect | hands-on | **CP4** — battery + distance live |
| 1:11–1:19 | Drive it | hands-on, on the floor | **CP5** — forward, turn, return, stop |
| 1:19–1:25 | Aim camera, capture | hands-on | **CP6** — a photo on screen |
| 1:25–1:30 | Battery care, pack down, next time | slides | batteries collected |

Checkpoints exist so the room can be scanned at a glance. Don't move on until
most of the room is at the same place; park stragglers with a neighbour who is
already through.

⚠️ **If several students arrive without an imaged card, the 0:24 block will
overrun.** Hand those students a spare pre-imaged card rather than letting the
room wait — the point of today is a working robot, not the imaging exercise.

**Cut in this order if you are behind:** the `robot_play.py` segment first (5 min,
slides 21–22), then CP6 (camera), then CP5 (driving) — opening lecture 1 with
driving is no loss. Never cut the battery-care slide.

`robot_play.py` earns its five minutes when it fits, though: it is the shortest
path from "I typed a command" to "the robot moved", it proves the hardware before
any laptop software is involved, and it is the fallback for any student whose
laptop will not run the console.

## Before the session

**Tell students to do this at home, and chase it:**

- [ ] Choose a robot name and image their SD card following the guide on slide
      13 — the hostname must match the name on their sticker
- [ ] Install **Raspberry Pi Imager** (~150 MB — a bad thing to download twenty
      times over one uplink on the day)
- [ ] Check `ssh -V` works in their terminal. macOS and Linux always do; Windows
      10/11 normally does, but an old build may need OpenSSH Client adding from
      Settings → System → Optional features
- [ ] Optional but a big time-saver: clone the console repo and run
      `python3 launch.py --check` at home, so the venv and paramiko are already
      in place before the session

**Bring:**

- [ ] 2–3 **spare pre-imaged cards** for students who arrive without one
- [ ] Spare microSD cards and a **card reader** — many laptops have no SD slot
- [ ] Stickers and a marker, for labelling robots
- [ ] Two or three spare charged battery packs

**Setup:**

- [ ] Router: **Smart Connect off**, separate SSIDs — robots on 2.4 GHz
      (`ShineLabs`), laptops on 5 GHz. A Pi Zero 2 W is 2.4 GHz only, and 40
      clients on one band will hurt.
- [ ] A **roster sheet** to write student → robot name on as they choose. Names
      are creative and unpredictable now, so this is the only record of which
      robot belongs to whom — you will need it all series
- [ ] Batteries charged. Two LEDs lit on every pack before students arrive.
- [ ] Gateway laptop up, `./scripts/status.sh` reports READY (see `slab-gw`)
- [ ] Wi-Fi name and password written on the board — **not** on a slide, since
      the deck is in a public repo. Students need these for Imager.
- [ ] Slack QR scans from the back of the room (test it on the projector, not
      just on screen)
- [ ] Rehearse once end-to-end on one robot; every placeholder filled

## Placeholders still to fill

| File / slide | What's needed |
|---|---|
| "Introduction" slide | instructor bio |
| `assets/dashboard.png` | screenshot of the finished dashboard |
| slide 21 | option numbers are from `robot_play.py` — re-check if that menu changes |
| 5 GHz SSID | laptop network name |
*(the setup-script and console commands are now filled in)*

## Things that will go wrong, and the answer

| Symptom | Cause | Fix |
|---|---|---|
| Imager never showed a customisation step | they clicked SKIP CUSTOMISATION | rewrite the card — without it there is no hostname, no Wi-Fi and no SSH |
| `ping <name>.local` fails | wrong Wi-Fi details entered in Imager | check hostname spelling first, then rewrite the card |
| First boot seems to hang | filesystem expansion + Wi-Fi join | give it two minutes before declaring it broken |
| `ssh` asks for a password they don't know | they forgot what they typed in Imager | this is why the slide says write it down; otherwise rewrite the card |
| `ssh` refuses with a host-key warning | card rewritten, same hostname | on their laptop: `ssh-keygen -R <name>.local` |
| Two robots share a name | duplicate not caught when chosen | rename one: `sudo hostnamectl set-hostname <newname>`, reboot, update the roster |
| Hostname rejected or `.local` never resolves | illegal name — spaces, capitals, underscores, emoji | lower case, letters/digits/hyphens only, no leading or trailing hyphen |
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
- Left/right (or space) moves through every slide — the deck is flat, so there
  are no vertical stacks and up/down do nothing
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

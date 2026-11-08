# Ariana Lounge — full desktop revamp for Chatterino7

Full revamp, not just themes — but the theme pack IS part of it.

## Hard rule

It still works exactly like unchanged Chatterino 7TV underneath. Same
behaviour, same features, nothing removed or changed underneath: Twitch +
Kick, 7TV / BTTV / FFZ, tabs, splits, highlights, notifications, plugins,
login, settings, chat sending. The revamp is additive / visual on top of
stock Chatterino7. The shelf / ticker / chips / Settings are additions
only, all toggleable, all defaulting to not breaking normal use — chips
insert, never auto-send; the ticker is text only; grid / focus / mini are
opt-in, never forced. If an Ariana extra would change or break a stock
behaviour, it was dropped or simplified instead. No stock feature was
removed or rewired to fit the theme.

Desktop only. No phone frame, no Device Style, no home screen hub, no
passcode / code screen, no notch / punch-hole. No new login, no OAuth, no
account change. No Ariana photo / face, no album artwork files — colours
and short lyric fragments (text only) only.

## What is in it

**Loading screen (shows on every open):** sir's supplied image
("ARIANA GRANDE CHATTERINO 7TV", Ariana Grande in a purple stage
outfit on a round platform) is byte-identical to the file
sir sent, never regenerated or recoloured — but it is NOT inside the
patch: the patch is text-only, and the JPG ships as a separate repo
file (`ariana-loading-screen.jpg` at the repo root). The workflow
copies it into `resources/ariana-loading-screen.jpg` before building
and checks its SHA-256 first, so Chatterino's resource generator
embeds it as `:/ariana-loading-screen.jpg`. (Run #1 lesson: a binary
JPG hunk inside the patch made `git apply` fail on the runner, and
the unchecked step then built stock Chatterino7 and shipped it as
Ariana Lounge.) On every app open it
covers the Main window full-screen, then fades out: 100% at 0s,
75% at 1s, 50% at 2s, 25% at 3s, 0% (gone) at 4s. A 1-second QTimer
steps the opacity by 0.25, plus a hard 4-second fallback hides it
no matter what, so it can NEVER stick on loading and block the
chats. The chats load underneath while it fades; it does not delay
or block startup, and mouse clicks pass straight through it. If
the image resource is missing, it hides immediately instead of
showing a black screen.

**Themes (the theme pack, included):** 9 built-in albums, in
`resources/themes/` inside the patch and in `themes/` here, copied
word-for-word from the theme pack — Sweetener, Positions, Eternal
Sunshine, 7 Rings, Thank U, Next, Dangerous Woman, Yours Truly,
My Everything, Christmas & Chill. Picking an album switches the theme
live, no restart.

**Shelf (Main window, left):** album buttons, Mini / Focus / Grid
buttons, a Spotify "♪ Ariana hub" button (opens her hub on the
Discovery Layer, no audio in Chatterino), and a countdown chip —
Ariana birthday June 26 + album anniversaries (Sweetener Aug 17,
Thank U, Next Feb 8, Positions Oct 30, Eternal Sunshine Mar 8).

**Ticker + chips (Main window, under the chats):** a thin lyrics
ticker that rotates album-specific fragments (star ☆ to pin a
favourite lyric first), 12 quick phrases + 6 reactions + 6 emote
shortcodes as chips. Tapping a chip INSERTS the text into the
selected split's input — it never auto-sends.

**Look (row tints, all toggleable):** own messages soft pink tint,
lyric fragments gold (needs Sparkles on), mod / VIP gold tint,
bot messages dimmed, cloud background wash, startup quote (one
short line, dismissible). Username recolouring is NOT in here — it
needs MessageLayoutElement surgery, so it was dropped per the hard
rule rather than rewiring stock painting.

**Memory:** per-channel album (Twitch and Kick stored separately,
off by default), morning / afternoon / night scheduler, quiet hours
(ticker pauses, chats keep working), favourite lyric pin, Save /
Load current look (one JSON file), Copy theme file, tour / dates
field that stays BLANK unless sir types dates in — never guessed.

**Modes (opt-in, stock pause only):** Focus — only the selected
split scrolls live, others pause with the stock ChannelView pause
(the same pause Space uses). Grid — same pause rule, focused tile
live; the tiles stay in their stock split layout (see limits).
Mini — narrow 380x700 window, ticker + chips hidden.

**Commands:** `/album <name>`, `/lyric` (system message, nothing
sent), `/ariana` (opens Ariana Settings).

**Shortcuts:** Alt+1 to Alt+9 switch album, Alt+L ticker, Alt+C
chips, Alt+S sparkles. The same actions are also bindable in
Settings → Hotkeys (`arianaAlbum…`, `arianaToggle…`).

**Settings:** one "Ariana" page in Settings with the album picker,
every toggle above, quiet-hours hours, grid size, tour dates, and
the Save / Load / Copy buttons — plus the background music section
below.

**Background music (in-app player, default OFF):** Qt Multimedia
`QMediaPlayer` + `QAudioOutput`. It plays ONLY the user's own mp3s
from the `ArianaMusic` folder under the app data directory
(`%APPDATA%\Chatterino2\ArianaMusic` on Windows) — no songs are
bundled in the patch, the repo, or the exe. 5 songs, in this order,
1 minute each, then back to the first, looping forever: bloodline,
Into You, 7 rings, Dangerous Woman, 34+35. A 60-second cutoff timer
runs while playing, so a file can never play past 60 seconds even
if a full-length file is in the folder. Controls: a small music bar
under the ticker (Play / Pause, Prev, Next, Mute, volume slider,
Now Playing title only) and the Ariana Settings section
(enable checkbox, "Background music volume" slider 0–100, status,
folder path, "Open music folder" button). Default OFF on first
launch — no surprise sound, stock behaviour unchanged. On / off
and volume are remembered across restarts; music only auto-plays
on startup if it was left on and the files are present. One volume,
two places to change it: the bar slider and the Settings slider
both write the one `arianaMusicVolume` setting (default 80), so
they are always in sync. 0 is mute; sliding back up un-mutes.
If the folder or any file is missing, the Settings page says so in
plain text and the player does nothing — no error popup, no
blocking chat. Song titles only. This is the ONLY Ariana audio
control — no stock Chatterino volume/audio behaviour is touched.

## Files

- `ariana-lounge.patch` — 4,175 lines in the file (33 files,
  +3,746 / −1), TEXT-ONLY, on clean
  SevenTV/chatterino7 at `910b01dd428c4ac042028708704278b93227491b`.
  The loading-screen JPG is deliberately NOT in the patch: a binary
  hunk broke `git apply` on the GitHub runner in run #1 (the step
  did not check the exit code, so the run built stock Chatterino7
  and shipped it under the Ariana name). The JPG ships as a separate
  repo file instead — see `ariana-loading-screen.jpg` below.
  Verified: `git apply --check` passes and `git apply` applies cleanly
  with no rejects on a fresh clone of that commit, `git diff --check`
  clean, 33 files land, and the JPG copy + SHA-256 check pass
  (copied file hashes to
  `049a088a309fdf03f1bdfdafc4bb6f18fccb198db2e6d2676496ce52080990e2`,
  identical to sir's supplied file).
  New files: `src/widgets/ArianaLounge.{hpp,cpp}`,
  `src/widgets/ArianaLoadingScreen.{hpp,cpp}` (loading screen,
  fades 25% a second, gone at 4s),
  `src/widgets/ArianaMusic.{hpp,cpp}` (background music player +
  music bar, QMediaPlayer + QAudioOutput),
  `src/widgets/settingspages/ArianaPage.{hpp,cpp}`,
  `src/controllers/commands/builtin/ArianaCommands.{hpp,cpp}`,
  9 theme JSONs in `resources/themes/`.
  (No `resources/ariana-loading-screen.jpg` in the patch any more —
  that file arrives via the workflow copy step.)
  Edited (additive only):
  `CMakeLists.txt` (Qt `Multimedia` component),
  `Settings.hpp` (music on/off + volume settings), `Theme.cpp`,
  `MessageFlag.hpp`, `MessageLayout.{hpp,cpp}`,
  `Window.{hpp,cpp}` (music bar + loading-screen hook on first show), `SettingsDialog.{hpp,cpp}`,
  `SettingsDialogTab.hpp`, `Split.cpp`, `CommandController.cpp`,
  `src/CMakeLists.txt` (ArianaMusic + ArianaLoadingScreen sources +
  `Qt6::Multimedia` link).
- `ariana-loading-screen.jpg` — sir's supplied loading-screen image
  (1024x572 JPEG, SHA-256
  `049a088a309fdf03f1bdfdafc4bb6f18fccb198db2e6d2676496ce52080990e2`),
  a separate repo file at the repo root. The workflow's "Copy
  loading-screen image" step copies it into
  `upstream/resources/ariana-loading-screen.jpg` before building and
  throws if the SHA-256 does not match, so a wrong or corrupt image
  can never ship silently. Never regenerate or recolour it.
- `build-ariana-lounge.yml` — GitHub Actions, adapted from the
  Fold-iPhone workflow (same Qt 6.9.3 / MSVC2022 / windows-2022 /
  conan 2.11.0 pattern, Setup Python BEFORE clone to avoid the
  recursive-symlink ELOOP, release-auth step skipped, same
  packaging). Qt install now also includes the `qtmultimedia`
  module (Qt cache key bumped to v2 so a cached Qt without it is
  not reused). Output: `Chatterino7ArianaLounge.exe` / `.zip`.
  The "Apply Ariana Lounge patch" step now fails the build if the
  patch does not land: it rejects any binary hunk in the patch,
  throws on a non-zero `git apply` exit code, checks
  `ArianaLounge.cpp`, `ArianaLoadingScreen.cpp`, `ArianaMusic.cpp`
  and `resources/themes/ArianaSweetener.json` exist, and throws
  unless exactly 33 files changed (counted via `git status`, since
  `git diff` hides the 19 new untracked files).
- `themes/` — the 9 theme JSONs (same files as in the patch).
- `ARIANA-LOUNGE-DESIGN.md` — the full design, More 1–4 all in.
- `concepts/` — 22 concept images (hero + 9 themes + 12 pieces).

## What was simplified or dropped (per the hard rule)

- **Grid 2x2 / 3x3 tile rearrangement:** simplified to the focus
  pause rule — focused tile live, others paused. Rearranging
  SplitContainer nodes would rewire stock layout, so the grid-size
  setting only labels the mode.
- **Tab groups by album and pinned chats:** dropped. They need
  Notebook internals (protected `Notebook::items` — the exact
  failure from Fold-iPhone Runs #8/#10).
- **Per-split colours (left Sweetener, right 7 Rings):** dropped.
  The theme is global in stock Chatterino; per-split themes need a
  new theme engine. Per-channel album covers the spirit: opening a
  remembered channel switches the theme.
- **Live-toast styling, Ctrl+F search colours, Copy as Ariana
  quote (right-click):** dropped. They need the notification widget
  / search widget / ChannelView context menu. Stock toasts, stock
  search, and the stock context menu are unchanged. Live
  notifications still use sir's one-toggle rule (Enable Toasts +
  Notify on any channel, list empty).
- **Username colours in the Ariana palette:** dropped. Needs
  MessageLayoutElement recolouring; the row tints above are the
  simple version that compiles.
- **Emote shelf:** simplified to shortcode chips (Kappa, PogChamp,
  LUL, KEKW, OMEGALUL, FeelsGoodMan) inserted as plain text and
  rendered by the stock emote providers. No new emote data invented.
- **Viewer count chip:** not added — stock `headerViewerCount`
  already shows the viewer count in the split header; it is left
  exactly as-is.
- **Own-message frame (rounded frame + initial circle):** simplified
  to the soft pink row tint. The frame would need MessageLayout
  bubble painting like the phone build; the tint keeps the feature
  without it.

## Build / install (once the repo + run exist)

The patch + workflow are ready here; the GitHub repo and Actions run
are still pending (workflow files are blocked via API and need the
website step — the main agent handles that next). When the run
succeeds (~24 min based on the Fold-iPhone Run #12), download
`Chatterino7ArianaLounge.zip`, unzip, run the exe inside with its
DLLs. Live Windows run still untested here, as with the other
Chatterino builds.

## Honest limits

- Compile is NOT proven here — `git apply` is verified clean, but
  no Windows build has run yet. The GitHub run is the compile test.
  The new Qt Multimedia dependency is the main compile risk: the
  workflow now installs the `qtmultimedia` Qt module, and the patch
  links `Qt6::Multimedia`. If that module fails to install, the
  fallback is a music bar that opens the user's local
  ArianaLoungeMusic player in the browser instead of playing
  in-app — that fallback is NOT built; it would be a patch change.
- Music plays through Qt Multimedia's Windows Media Foundation
  backend, which is how stock Windows plays mp3s. If Media
  Foundation is missing on a PC, music will not play; the rest of
  Chatterino is unaffected. No songs are bundled — sir must copy
  his own 5 trimmed mp3s into `%APPDATA%\Chatterino2\ArianaMusic\`
  with the exact names `01-bloodline.mp3`, `02-into-you.mp3`,
  `03-7-rings.mp3`, `04-dangerous-woman.mp3`, `05-34-35.mp3`.
- NoFreeze, !pause, Anonymous mode, and Old People UI are NOT in
  this patch — they stay separate packs, untouched.

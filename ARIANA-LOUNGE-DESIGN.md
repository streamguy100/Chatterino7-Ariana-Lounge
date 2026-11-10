# Ariana Lounge — all-new desktop Chatterino idea (NO phone stuff)

Status: DESIGN ONLY, 2026-11-07/08. Phone build scrapped per sir — no Fold, no iPhone, no Device Style, no home screen hub, no passcode/code screen, no phone frame, notch, or punch-hole.

## Idea in one line
Normal desktop Chatterino7 window, fully Ariana-themed. Same chats, same tabs/splits, just an Ariana lounge look and a few Ariana extras on top.

## Pre-have — already in hand, do NOT remake
- Base Chatterino7 (Twitch + Kick, 7TV / BTTV / FFZ, highlights, notifications, plugins, tabs and splits)
- Chatterino NoFreeze pack (6 keys only, backup first)
- !pause media plugin (Lua + Windows watcher, own account only by default)
- Anonymous view-only mode (built-in Anonymous account; Lua helper only posts banner/check)
- Old People UI themes (OldPeopleDark / OldPeopleLight) as a reference for how a theme pack ships
- Chatterino7 Fold-iPhone build exists separately and is NOT part of this — do not reuse its phone code here

## The 6 album themes (desktop theme JSONs, colours only)
Copy the existing Chatterino theme JSON structure (iPhoneLight/Dark as reference). No Ariana photo/face, no copyrighted images — colours, text and simple shapes only.

1. Sweetener — cloud pink #FFB6D5 / white #FFFFFF, accent #FF6FA5, soft grey text
2. Positions — lavender #C9B6FF / white, accent #8B6FE8
3. Eternal Sunshine — cream #FFF6E5 / soft yellow #FFD966, accent #E8A800
4. 7 Rings — black #0D0D0D / gold #D4AF37, accent gold, white text
5. Thank U, Next — hot pink #FF2E88 / black #111111, accent hot pink
6. Dangerous Woman — deep purple #2A0A4A / black, accent #9B5CFF

Each theme: window, splits, tabs, messages, scrollbars, input, links, live indicator — same keys as the reference JSONs.

## Layout — desktop, not phone
- Normal Chatterino window, normal tab bar on top, normal splits.
- Left album shelf (new, simple): a narrow vertical strip listing the 6 albums. Clicking one switches the theme live. No home screen, no app icons, no restart needed for colour switch.
- Chat stays in the middle, input pinned at the bottom as normal.

## New extras (simple only, so they compile / run)
- Lyrics ticker: one thin line along the bottom of the window (above input, toggleable). Rotates short public fragments only: "thank u, next", "7 rings", "positions", "yes, and?", "sweetener". Text only, no song files, no audio.
- Quick-send chips: a row above the input, toggleable. Chips: "thank u, next ♡", "7 rings", "positions", "yes, and?". Tapping a chip INSERTS the text into the input — it does NOT auto-send.
- Sparkles toggle: subtle sparkle highlight on mentions / highlighted messages only. Off by default if it risks performance; NoFreeze rules still apply.
- Own messages: soft pink tint. Others: theme background. Mentions: pink/gold highlight. No timestamps change — keep Chatterino's normal timestamps unless sir asks otherwise.
- Settings: one "Ariana" section in Settings with Album picker, Lyrics ticker on/off, Quick chips on/off, Sparkles on/off. No new Device Style tab, no Code Screen tab.

## What is NOT in this idea
- No phone frame, no Device Style switch, no home screen, no passcode lock.
- No Ariana photo, no face, no album artwork files. Colours + words only.
- No new login, no OAuth, no account change. Twitch/Kick accounts stay as they are.
- No media pausing change — !pause stays as-is.

## Build options (for sir to pick)
A. Theme pack only — 6 theme JSONs + a short README. Drop into Chatterino Settings → Appearance → Themes. Fastest, no compile, no GitHub run.
B. Full desktop revamp — theme pack + album shelf + lyrics ticker + quick chips + Ariana Settings section, as a patch on clean Chatterino7 910b01d + a GitHub Actions workflow (same Qt 6.9.3 / MSVC2022 pattern as the Fold-iPhone build). Needs a GitHub run (~24 min based on Run #12) and a live Windows test.

## Limits to state plainly
- Lua cannot restyle Chatterino or draw new UI by itself; the shelf/ticker/chips need the C++ patch (option B). Option A is themes only.
- Live Windows build/test still untested here, as with the other Chatterino builds.
- If a fancy shelf/ticker implementation will not compile, use the simple version keeping the same features (sir's rule, 2026-11-08).

## More — added 2026-11-07 at sir's "More"
- Chat-only grid / stack: MultiStream-style grid, chat only, no video — 2x2 / 3x3 tiles, each tile a different chat AND a different album theme. Inactive tiles pause scrolling (NoFreeze lesson: all-live tiles freeze), only the focused tile scrolls live.
- Per-channel album: assign an album to a channel and it remembers — e.g. one streamer always opens in Positions, another in 7 Rings.
- Album of the day / era mode: auto-switches theme by day, or by time — Sweetener mornings, Eternal Sunshine afternoons, 7 Rings nights. Toggleable.
- Spotify link: Now Playing bar for Ariana, linked to her hub on his Spotify Discovery Layer (one of the five marquee artist hubs there). Click opens the hub. No audio in Chatterino itself.
- Live toast, Ariana-style: when a followed streamer goes live, a pink/gold toast in the album colour of that channel, not the plain Chatterino one.
- Lyric highlights: when chat types a known Ariana fragment ("thank u, next", "7 rings", "break free", "into you"), that message gets a sparkle highlight.
- Quick phrases expanded to 12, editable in Settings: thank u, next ♡ / 7 rings / positions / yes, and? / break free / into you / sweetener / moonlight / cloud ☁ / bow 🎀 / ring 💍 / eternal sunshine ☀
- Reaction row: cloud ☁, bow 🎀, ring 💍, moon 🌙, sun ☀, heart ♡ — quick insert into input, same insert-not-send rule as chips.
- Focus mode: one chat big in the centre, other open chats paused in a side strip, tap to swap focus. Helps the freeze — only the focused chat renders live.
- Cloud background toggle: soft cloud tint behind chat, on/off, kept light so text stays readable.
- Search filter: filter current chat by a word/phrase, Ariana lyrics included.

## More 2 — added 2026-11-07 at sir's "Keep this list but add to it" (kept everything above)
- 3 extra album themes, total 9: Yours Truly (cream + soft red), My Everything (black + white + silver), Christmas & Chill (deep red + pine green + white, winter only / toggleable). Core 6 stay as the main set.
- Chat commands (typed in input, no new UI needed): /album <name> switches theme, /lyric drops a random Ariana fragment into input, /ariana opens the Ariana Settings section.
- Username colours in Ariana palette: usernames cycle soft pink / lavender / gold / cream instead of Chatterino defaults, toggleable, readable on both light and dark themes.
- Ticker, album-specific: lyrics rotate from the album currently picked — Sweetener shows Sweetener lines, Positions shows Positions lines, etc. Still text only.
- Countdown chip on the home bar: Ariana birthday June 26, plus album anniversaries (Sweetener Aug 17, Thank U, Next Feb 8, Positions Oct 30, Eternal Sunshine Mar 8). Small text chip, toggleable, no popups.
- Pinned Ariana chats: pin up to 3 chats to the top of the tab bar, with a small ♡ on the tab.
- Large-text Ariana versions: every theme also ships in a Large variant (font size 20, like Old People UI) — ArianaSweetener-Large etc. Same colours, bigger text.
- Share theme: one button in Ariana Settings — "Copy theme file" — copies the current theme JSON so it can be shared, no account needed.
- Slow / hype indicator: when a chat goes fast, the tab shows a small ☁ "cloudy — fast chat" dot; when slow, a ♡. Just a visual, no auto-pause.
- Mod / VIP sparkle: mods and VIPs get a tiny gold sparkle next to their name in Ariana mode, toggleable.
- Kick + Twitch together: album assignment works per channel on both platforms, same rule as the per-channel account check — Twitch album does not leak into Kick and vice versa.

## More 3 — added 2026-11-07 at sir's "More add" (kept everything above)
- Mini mode: compact Ariana window for a second monitor — one chat only, narrow, album theme kept, ticker + chips hidden to save space, tap to expand back to full.
- Own-message frame: your messages get a soft pink/gold rounded frame with your initial in a small circle, same per-channel account rule as before — Twitch name on Twitch, Kick name on Kick, nobody framed when logged out / anonymous.
- Highlight words in Ariana colours: your Chatterino highlight words show in pink/gold instead of the default, with a small ♡ marker. Settings stay the same, only the look changes.
- Live notifications, all open chats: uses the existing one-toggle rule sir already has — Enable Toasts on + Notify on any channel on, list empty — but toasts are styled in the current album colours, with the channel's album on the toast.
- Emote shelf: a small row above input showing your most-used 7TV / BTTV / FFZ emotes in that chat, tap to insert. No new emotes, just quick access to the ones you already use.
- Chat search, Ariana-style: Ctrl+F search box in album colours, with lyric fragments as searchable presets.
- Tour / dates chip: small text line in Ariana Settings showing Ariana's next public dates if sir supplies them — blank if not supplied, never guessed. Same blank-not-guess rule as the Creator Book.
- Theme scheduler: pick a theme for morning / afternoon / night and it switches on its own, or turn it off and stay on one album.
- Split colours: in a 2-split tab, left split and right split can have different album themes at once — e.g. left Sweetener, right 7 Rings.
- Export chat look: "Save current look" in Ariana Settings writes the current theme + toggles to one file, so it can be restored after a reinstall.
- Quiet hours: ticker + sparkles + live toasts pause during hours sir sets, chats themselves keep working.

## More 4 — added 2026-11-07 at sir's "More and what we got so far" (kept everything above)
- Tab groups by album: group open chats under an album heading in the tab bar — Sweetener group, Positions group, etc. Collapse a group to hide its tabs.
- Startup quote: one short Ariana line on launch, dismissible, in the current album colour — text only, no popup blocking chats.
- Keyboard shortcuts: Alt+1 to Alt+9 switch album, Alt+L toggle lyrics ticker, Alt+C toggle quick chips, Alt+S toggle sparkles. Listed in Ariana Settings.
- Viewer count chip: live viewer count in the chat header, in the channel's album colour, updates with the normal Chatterino count — no new count invented.
- Bot / spam dimming: messages from known bots dim to 50% in Ariana mode, toggleable, so real chat stands out.
- Chat pause button, per tile: a small ⏸ on each chat tile in the grid — pauses that tile only, others keep going. Same pause idea as Space in the freeze fix, but per tile.
- Copy as quote: right-click a message → "Copy as Ariana quote" — copies it with a ♡ prefix and the album name, for pasting elsewhere.
- Favourite lyric: star a lyric fragment in the ticker to pin it as your favourite — it shows first in the rotation until unstarred.
- Window remember: Ariana Lounge remembers window size, position, and last album on close, and restores them on open.

## More 5 — added 2026-11-07 at sir's "All more and show concept image 1 Image per every piece" (kept everything above)
- All More batches 1-4 are IN — nothing cut, this is the full list.
- Concept images: 1 image per theme piece (9 themes), UI mockups only — colours, chat bubbles, album shelf, ticker, chips. No Ariana photo/face, no album artwork.
- Concept image list: Sweetener, Positions, Eternal Sunshine, 7 Rings, Thank U, Next, Dangerous Woman, Yours Truly, My Everything, Christmas & Chill.

## Files planned (not built yet — awaiting sir's pick)
- workspace/chatterino-ariana/themes/ArianaSweetener.json etc. (6 files)
- workspace/chatterino-ariana/README.md (theme pack + revamp spec)
- workspace/chatterino-ariana/ariana-lounge.patch (option B only)
- workspace/chatterino-ariana/build-ariana-lounge.yml (option B only)

## Built 2026-11-07 — theme pack only, NO new build (sir: "Not new chatterino build using chatterino 7tv")
- Option A, for the existing Chatterino with 7TV. No exe, no patch, no GitHub run.
- 9 theme JSONs in workspace/chatterino-ariana/themes/ (ArianaSweetener, ArianaPositions, ArianaEternalSunshine, Ariana7Rings, ArianaThankUNext, ArianaDangerousWoman, ArianaYoursTruly, ArianaMyEverything, ArianaChristmasAndChill), all JSON-validated, same schema/structure as OldPeopleDark/Light.
- Deliverable: ~/workspace/your_files/ArianaLoungeThemes/ + ArianaLoungeThemes.zip (306KB) — Themes/ (9 JSONs) + README.md + preview.webp (the Ariana-in-Chatterino image).
- Install: copy JSONs to %APPDATA%\Chatterino2\Themes, restart, Settings > Appearance > Theme > Custom: Ariana…
- Limits: themes are colours only — no album shelf, ticker, chips, or Ariana photo inside Chatterino; those still need a C++ patch / new build. Live Windows test still pending.

## Built 2026-11-07 — FULL desktop revamp, theme pack included (sir: "full revamp not just theme but theme is part of it")
- Hard rule: still works exactly like unchanged Chatterino 7TV underneath — same behaviour/features, nothing removed or rewired; revamp + themes are additive/visual only, all extras toggleable/opt-in. Chips insert, never auto-send; ticker text only; grid/focus/mini opt-in, never forced.
- `ariana-lounge.patch` — 3,220 lines, 28 files (+2,840/−1) on clean SevenTV/chatterino7 910b01dd428c4ac042028708704278b93227491b. Verified twice: `git apply --check` passes and `git apply` applies cleanly with no rejects on a fresh clone of that commit. New: ArianaLounge.{hpp,cpp} (shelf, ticker, chips, lyrics, countdown, scheduler, quiet hours, per-channel memory), ArianaPage.{hpp,cpp} (Settings page), ArianaCommands.{hpp,cpp} (/album, /lyric, /ariana), 9 theme JSONs in resources/themes/ (byte-identical to themes/). Edited, additive only: Settings, Theme, MessageFlag, MessageLayout, Window, SettingsDialog, Split (per-channel album hook), CommandController, CMakeLists.
- In: shelf, ticker, chips/reactions/emote shortcodes, Ariana Settings, commands, Alt+1-9/L/C/S shortcuts + Hotkeys actions, own-message pink tint, lyric/mod-VIP gold tints (sparkles-gated), bot dim, cloud wash, startup quote, countdown, scheduler, quiet hours, per-channel album (Twitch/Kick separate), favourite lyric, Save/Load look, Copy theme file, Spotify hub link, Focus/Grid pause (stock ChannelView pause, focused tile live), Mini mode.
- Simplified/dropped per the hard rule (see README.md): grid tile rearrangement → pause rule only; tab groups + pinned chats dropped (Notebook protected internals, the Fold #8/#10 failure); per-split colours dropped; live-toast styling, Ctrl+F colours, right-click Copy-as-quote dropped; username palette dropped (element-level recolour); emote shelf → shortcode chips; viewer count = stock headerViewerCount, untouched.
- `build-ariana-lounge.yml` — adapted from build-fold-iphone.yml (Qt 6.9.3 / MSVC2022, Setup Python before clone, release-auth skipped). Output Chatterino7ArianaLounge.exe / .zip.
- `README.md` in this folder explains install, limits, and every simplification.
- Still pending: GitHub repo + Actions run (workflow files blocked via API, needs the website step — main agent next). No compile proven yet — the run is the compile test. Live Windows run still untested. NoFreeze, !pause, Anonymous, Old People UI stay separate packs.

## Background music — added 2026-11-07 (sir: "add to the chatterino 7tv u making")
- In-app player, Qt Multimedia QMediaPlayer + QAudioOutput (new files src/widgets/ArianaMusic.{hpp,cpp}). Patch now 3,955 lines / 31 files (+3,545/−1), verified again on a fresh worktree at 910b01d: git apply --check PASS, git apply PASS, git diff --check clean.
- Folder: %APPDATA%\Chatterino2\ArianaMusic\ — sir drops any mp3s of his own there. No mp3s bundled in patch/repo/exe. Empty or missing folder → plain note in Ariana Settings, player does nothing, no popup.
- Folder-based (changed 2026-11-10, sir: "remove pre added and make it a folder based mp3 player where it only plays from mp3 in a folder"): the 5 fixed songs are gone — no TITLES/FILES lists, no 60-second cutoff, no cut timer. Whatever *.mp3 files are in the folder, filename order (case-insensitive), each song in full, after the last back to the first, looping forever. Rescanned on every navigation/start/enable, so files dropped in while the app runs are picked up. Track title = the filename without .mp3 (dashes/underscores shown as spaces). Song titles only, no lyrics anywhere in the music feature.
- Controls: music bar under the ticker (Play/Pause, Prev, Next, Mute, volume slider, Now Playing title) + Ariana Settings (enable checkbox, "Background music volume" slider 0–100, status, folder path, "Open music folder"). Default OFF, remembered on/off + volume across restarts, auto-plays on startup only if left on and files are present. One volume, two sliders, same setting (default 80); 0 = mute, sliding back up un-mutes. Only Ariana audio slider — no stock Chatterino volume/audio behaviour touched.
- Build changes: Qt `Multimedia` added to top-level CMakeLists find_package + `Qt6::Multimedia` link in src/CMakeLists.txt; workflow installs the `qtmultimedia` Qt module (cache key bumped v1 → v2). Compile still NOT proven — the GitHub run is the test; music plays via Windows Media Foundation on Windows.

## Loading screen — added 2026-11-07 (sir supplied the exact image)
- File: `ariana-loading-screen.jpg` in this folder (1024x572 JPEG, SHA-256 `049a088a309fdf03f1bdfdafc4bb6f18fccb198db2e6d2676496ce52080990e2`) — "ARIANA GRANDE CHATTERINO 7TV" on the left, Ariana Grande in a purple stage outfit on a round platform, purple/pink stage lights. Used word-for-word in the patch as `resources/ariana-loading-screen.jpg`; the generated concept fade image is NOT used. The earlier generated loading-screen concept (5-stage fade image) is superseded by sir's supplied image.
- Shows on every app open, full Main window, then fades: 100% at 0s, 75% at 1s, 50% at 2s, 25% at 3s, 0% (gone) at 4s. New files `src/widgets/ArianaLoadingScreen.{hpp,cpp}`: a child overlay widget that paints the image (scaled to fill, centre-cropped), a 1-second QTimer stepping opacity by 0.25, plus a hard 4-second single-shot fallback that hides it no matter what — it can NEVER stick and block chats. Chats load underneath; it does not delay or block startup; mouse clicks pass through it. If the image resource is missing it hides immediately instead of a black screen. Hooked in `Window::event()` on the first `QEvent::Show` of the Main window only, guarded so it never reappears on later shows.
- Embed: no CMake change needed — Chatterino's `cmake/resources/generate_resources.cmake` globs everything under `resources/` into the auto-generated Qt resource file, so the JPG is embedded as `:/ariana-loading-screen.jpg` once the workflow copies it there (it ships as a separate repo file, NOT inside the patch — a binary JPG hunk broke `git apply` in run #1 and silently shipped stock Chatterino7). Patch now 36 files, +3,952/−1 (4,406 lines, text-only). Verified on a fresh worktree at 910b01d: `git apply --check` PASS, `git apply` PASS, `git diff --check` clean, 36 files land, JPG copy + SHA check PASS. Compile still NOT proven — the GitHub run is the test.

## Ariana figure — added 2026-11-10 (sir sent a screenshot of the run #7 build with the figure pasted bottom-left: "just add that")
- File: `ariana-figure.png` in this folder (202x600 PNG, transparent, SHA-256 `d2a47bfb501d3f22154a7371d9382dc0fb4cb6907ceac1438e8a5626a44e1906`) — sir's supplied beach photo (pink bikini top, pink thigh-high fishnet stockings, pink platform heels, high ponytail, holding a bucket, "SUMMER VIBES" text) with the beach background removed by rembg (u2netp — the full u2net model OOM'd the VM; faint bucket ghost cleaned by hand in the mask). Figure only, head to feet, no beach/sand/palm/text left. The figure herself is untouched — same body, same face; only the background was removed. Same separate-repo-file rule as the loading-screen JPG (never baked into the patch — the patch stays TEXT-ONLY); the workflow copies it into `upstream/resources/` with a SHA-256 check, and the same `generate_resources.cmake` glob embeds it as `:/ariana-figure.png`.
- New files `src/widgets/ArianaFigure.{hpp,cpp}`, modelled on ArianaLoadingScreen: a child overlay of the Main window (NOT in a layout), 300px tall on screen, bottom-left (8px from the left, feet ~100px above the bottom, like his screenshot), mouse events pass straight through (WA_TransparentForMouseEvents) so chat stays clickable, refits on parent resize via an event filter. Created once on the first `QEvent::Show` of the Main window, before the loading screen. New setting `arianaFigureEnabled` (default on) + checkbox on the Ariana Settings page ("Ariana figure — standing Ariana at the bottom-left of the Main window"); the figure shows/hides live when toggled. Hidden when the resource is missing.

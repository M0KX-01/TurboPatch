# How TurboPatch works

The detailed reference: every page and setting, how each integration works, the files TurboPatch
creates, building, testing and publishing. For what TurboPatch is and how to get it, see the
[README](../README.md).

## Pages

The tabs, top to bottom: Library, Mods, Tools, Shaders, Display, Input, Hardware, Performance,
Community, and Settings at the bottom. The arrows at the top left (or the mouse's side buttons,
Alt+Left / Alt+Right) go back and forward through the pages you visited, like a browser; they turn
around in right-to-left languages.

| Page | What it does |
|---|---|
| **Library** | Finds games from Steam, Epic, GOG, EA app, Ubisoft Connect, Battle.net, Rockstar and the Xbox app / Game Pass, plus any folder you add (D:\Games and its subfolders: DRM-free, portable, emulators). List, cover-grid (centered) or banner view (wide hero art, at most two per row, with the game's logo from Steam or SteamGridDB on top), with a divider you drag to size the game list and the details pane (remembered per view); each game shows its store's icon on a square badge, taken from the launcher on your PC. Filter by store / favorites / recently played / collection / hidden (each with its icon), sort, search. Right-click (or select several) to play, rename, customize, favorite, add to a collection, reset or remove. Covers, banners and logos download automatically (Steam, or SteamGridDB with a free key); *Customize* lets you pick your own. Steam games show their **achievements** (5 of 39, read from Steam's files on your PC, or exactly from your Steam account if you connect it). Under the banner: **Play** (or **Suspend** / **Resume** while it runs), **Customize**, **Mods**, **Nexus Mods** (the game's page on nexusmods.com, shown only when TurboPatch can find it reliably), **Game folder** and **More**. **Find save folder** finds where a game keeps its saves (Ludusavi's community list) and backs them up. Playtime and last played are tracked. *While playing* settings: Afterburner profile, RTSS frame limit, power plan, monitors to turn off, Windows HDR on, monitor brightness (main display or all), start Lossless Scaling, HidHide on, extra programs. Every game uses the shared **Settings for all games** unless you switch it to **Only this game**; both can be reset. **Play** applies them first, shows a launch card (cover, name, playtime, achievements; it never takes focus), then starts the game; games started from their own launcher are detected too. Everything is restored when the game closes. A running game can be **suspended** (frozen, using no CPU or GPU) and resumed where it was, from its page, the tray, a keyboard shortcut or a controller button combination. **Big Picture** (the button at the top right, F11, or Menu on a controller): the library full screen for a TV or the couch, made for an Xbox-compatible controller: the selected game large at the top with its art and logo, Play / Options / Favorite, categories switched with LB / RB, big covers browsed with the d-pad or stick, soft click sounds while browsing; questions TurboPatch asks work with the controller too. An optional screensaver (after 1, 5 or 10 minutes) shows your games' art full screen on black, fading through black from game to game, with the game's name and the time moving from corner to corner so nothing burns into a TV or OLED; Settings → Library → Artwork gets 3840×1240 banners for all games to keep it sharp on a 4K TV. |
| **Mods** | Per game: ReShade (add-on build, DLL name picked from the game's graphics API), RenoDX HDR mods matched from the official mod list (plus the Unreal/Unity engine-wide mods), ReLimiter, BFI Presenter, DLSS DLL swap with backup (Super Resolution and Ray Reconstruction update to NVIDIA's newest in one click), **DLSS 5 neural rendering** through ReShade add-ons (renodx-dlss for 64-bit games that have DLSS; DLSS5-Feeder for games without DLSS, 32-bit, Vulkan and OpenGL), and one shared shader library for all games. Warns about conflicts (two frame limiters, BFI with frame generation…). |
| **Display** | Turn monitors off/on in software, toggle Windows HDR per monitor, a brightness slider per monitor (DDC/CI or a laptop's built-in screen), save and apply layouts. Monitor and HDR changes roll back after 15 s unless you confirm. |
| **Performance** | Live FPS and frame time from RTSS, frame-limiting advice, Lossless Scaling, Windows power plans (incl. adding Ultimate Performance). |
| **Shaders** | Shader compilation stutter, fixed ahead of time with SCSKiller: lists your DirectX 11/12 games with their status (compiled, ready, needs compiling again after a driver update, needs a recording, anti-cheat) and how badly each is known to stutter, then compiles one game or all that are ready into the GPU driver's cache, with a live progress line and Stop. Optionally, **Play** offers to compile first when a known stutterer isn't compiled. NVIDIA and AMD. |
| **Hardware** | PC summary, apply Afterburner profiles 1–5, the profile to return to after games, Fan Control, and the CPU tuning tool that fits your processor. |
| **Input** | Live view of the four Xbox controller slots, then the DS4Windows → HidHide → Steam Input → x360ce path for making any pad work. HidHide hiding on/off and per-device hide/unhide. |
| **Community** | Presets for the game matched to your GPU tier, a preview of every value that changes, apply with backup, restore, and "Share my settings". **Sources** are listed on the page with an on/off switch each: built-in examples, *My presets* (save a game's current settings as your own preset in one click), and any GitHub repository (paste its github.com link), web address or folder laid out like the template in `community-configs/`. *Export the template…* writes that template to a folder to start your own. |
| **Tools** | Status of every external program, Open / Download / Set path, and the activity log. |
| **Settings** | **Appearance**: 12 built-in themes (6 dark, 6 light) and your own: frosted, blurred or clear glass, or a solid color; the glass color with its opacity, grain texture, live previews that show each theme's glass, color and background, background effect (waves / aurora / embers / gradient / your picture) with strength and speed, one accent or per-tab colors; import and export. **Language**: 11 languages, game titles in your language, translated mod and tool names. **Library**: game folders to scan, when to scan (manual, at start, hourly), watch folders for new games, which stores to read, SteamGridDB key, achievements (optional Steam Web API key). **In game**: the launch card; suspend and resume (keyboard shortcut, controller buttons and how long to hold them); **ReShade's look in every game** (style or your own colors, opacity, corner roundness, font and size, FPS counter color and size, with a live preview), kept in every game with ReShade. **Sounds**: three sets of sound effects (Glass, Pulse, Arcade), volume, which sounds play, quiet while a game runs. **Updates**: checks every program and mod TurboPatch works with for a newer version (once a day at start, or *Check now*); programs show installed vs. latest, mods show how many games have an older copy, with *Update all*. **General**: automation, start with Windows (no UAC prompt), tray. **Backup**: everything in one zip. **About**: what TurboPatch is and aims to do, and every project and person it builds on, with links. |

## Look and feel

- **Themes** (Settings → Appearance), 12 built in.
  Dark: *Default* (OLED black: blurred glass under black at alpha 255, waves at 10% strength and
  35% speed, no grain), *TurboPatch Dark* (frosted glass with a light black color), *BlurMica Glass*
  (BlurMica's dark values: black at alpha 120), *Midnight* (aurora), *Mono Purple* and *Ocean Deep*.
  Light: *Light Glass*, *Paper*, *Frost*, *Sakura*, *Mint* and *Sand*.
  Change anything on a built-in theme and TurboPatch makes your own copy automatically (the original
  stays as it is); changes show instantly and themes can be exported as `.tptheme.json` files.
- **Glass:** *Frosted* (Windows 11's acrylic: the desktop shows through softly, like milky glass),
  *Blurred* (see-through, blurred, also on Windows 10), *Clear* (see-through, no blur) or a *Solid
  color*. (Mica was removed; themes that used it now use frosted glass.) TurboPatch draws its own
  title bar, so the glass and its color cover the whole window as one sheet, title bar included
  (like Windows 11 Settings). Dragging, double-click to maximize, Snap Layouts on the maximize
  button, Win+arrow keys and Alt+F4 work as usual. The glass color's opacity (A, 0–255) sets how
  strongly it covers the glass; lower shows more of what's behind the window. Frosted glass always
  keeps Windows' own milky layer, so for see-through glass choose *Blurred* or *Clear* (keep some
  color with *Clear* so text stays readable). On Windows 10, frosted glass shows as blurred glass
  with a little extra color.
- **The same look in the background:** the window keeps its glass and title when another window is
  in front (Windows would otherwise turn frosted glass solid and fade the title); the animated
  background keeps moving while the window can be seen, and pauses while it's minimized, in the tray
  or a game runs.
- **Edits show at once:** color and slider changes are applied once per frame (they used to queue
  up and land late), a typed color applies as soon as it's complete, and Windows is told to redraw
  the frame when the glass changes.
- **Theme previews** are drawn live from each theme's settings (glass over a sample desktop, glass color,
  background effect, grain and accent), so they look like the theme instead of a fixed picture.
- **Grain texture:** an optional fine film grain over the glass (0–100 %; 100 % is as strong as it
  stays pleasant), drawn at the monitor's real pixel size so it stays sharp at any display scale.
  Themes saved with the old *noise* value are converted automatically.
- **Touch screens:** tap, drag-to-scroll and the library divider work with touch and pen (WPF's
  Windows pointer input is switched on).
- **Selected tab** is solid (no see-through), tinted with its accent, with the glow around it.
- **Accent glows:** every tab and tool has its own color (or one color everywhere, per theme):

  | Area | Color |
  |---|---|
  | Library | turquoise (#40E0D0) |
  | Mods / ReShade | blue (shaders light blue, RenoDX gold, ReLimiter cyan, BFI Presenter ice white, DLSS green) |
  | Display / monitor control | red |
  | Performance / RTSS, Hardware / MSI Afterburner | purple (Lossless Scaling pink, power plan orange, fans teal, CPU tools orange-red) |
  | Input / controllers | green |
  | Community | amber |
  | Shaders / SCSKiller | fuchsia |
  | Tools (TurboPatch) | orange |
  | Settings | slate |

- **Sound effects** (Settings → Sounds): *Pulse* (rounded synth blips, the default, at 25% volume),
  *Glass* (soft chimes) or *Arcade* (8-bit beeps), made for TurboPatch (`tools/make_sounds.py`), for buttons and switches,
  page changes, results and notifications, and a game starting, being suspended or resumed. Volume
  and each kind of sound can be set; while a game runs only the game sounds play.
- **Backgrounds:** waves (pure vector Bézier curves with crisp crest lines, built at the window's
  real pixel size), aurora, embers, a calm gradient, or your own picture (optionally blurred). All
  animations run at 30 fps, only move pre-drawn shapes, and stop completely while a game is running,
  when the window is minimized or in the background, or when Windows animations are off.
- **4K:** per-monitor DPI aware; pictures are decoded at the monitor's real resolution (and again
  if the window moves to a monitor with a different scale); banners use 1920-pixel hero art instead
  of Steam's small headers; text uses true glyph shapes on high-DPI screens.

## Languages

Settings → **Language** switches the whole app instantly, no restart: English, العربية (Arabic),
Türkçe, Русский, Deutsch, 日本語, 简体中文 (Simplified Chinese), Español, Svenska, Bahasa Indonesia
and Tiếng Việt. On first start TurboPatch uses your Windows display language if it's one of these.

- **Arabic** turns the whole interface right to left (navigation on the right, mirrored layouts);
  paths, URLs, keys and launch options stay left to right.
- Each language uses fonts that contain its script (Yu Gothic UI for Japanese, Microsoft YaHei UI for
  Chinese, Segoe UI for Arabic), and dates and numbers follow the language (Arabic uses the
  Gregorian calendar).
- Plurals follow each language's rules (Russian 1 / 2–4 / 5+, Arabic's six forms, none in Japanese,
  Chinese, Indonesian and Vietnamese).
- **Show game titles in my language** (off by default): uses the game's official title from the
  Steam store when the publisher set one for your language.
  Titles are never machine-translated; games without an official localized title keep their
  original name, and names you set yourself always win. Searching and artwork still use the original
  title, so both work in any language.
- **Translate mod and tool names** (off by default): brand names stay searchable, so this shows a
  short description in your language with the original in brackets, e.g. *Bildratenbegrenzer
  (ReLimiter)*. Off shows the original names only.

Translations live in `src/TurboPatch.Core/Localization/Strings/<language>.<n>.json` (embedded in the
app). The key is the English text; a value is either the translation or, for counted text, an object
with the language's plural forms (`zero`, `one`, `two`, `few`, `many`, `other`). Anything missing
falls back to English. To fix a translation, edit the JSON and rebuild. To check all languages after
changing UI text, run:

```
python tools/l10n/extract.py             # lists every translatable English string (tools/l10n/keys.json)
python tools/l10n/check_translations.py  # coverage, {0} placeholders and plural forms per language
```

## Build and run

(To make a zip to give to other people, see [Make a ready-to-share copy](#make-a-ready-to-share-copy) below.)

You need Windows 10 or 11 (x64) and the **.NET 8 SDK**
(https://dotnet.microsoft.com/download/dotnet/8.0). Visual Studio 2022 with the
".NET desktop development" workload works too.

**Easiest:** double-click `build.cmd`. When it finishes, the `publish` folder opens with `TurboPatch.exe` in it.

**PowerShell alternative:** open PowerShell in this folder and run

```powershell
powershell -ExecutionPolicy Bypass -File .\build.ps1                 # needs .NET 8 on the PC
powershell -ExecutionPolicy Bypass -File .\build.ps1 -SelfContained  # larger exe, runs anywhere
```

then run `publish\TurboPatch.exe`. Windows asks for administrator rights (see below).

**Visual Studio:** open `TurboPatch.sln`, make sure *TurboPatch.App* is the startup project, press F5.
Visual Studio offers to restart as administrator because the app requires it.

**Command line, for development:** from an administrator terminal, `dotnet run --project src\TurboPatch.App`.

### Why administrator

Game folders under Program Files, RTSS profiles and MSI Afterburner need admin rights; running the
TurboPatch elevated avoids a UAC prompt for every action. Games themselves are still started as your
normal user (through their store, or through Explorer). *Settings → Start with Windows* uses a
scheduled task, so there's no prompt at sign-in either.

That task starts TurboPatch with full rights at every sign-in, so whoever can replace `TurboPatch.exe`
gets those rights too. Keep the exe in a folder only administrators can change (such as
`C:\Program Files\TurboPatch`); TurboPatch asks before creating the task when the exe is somewhere else.

### Tests

The logic that touches files, the registry and processes is covered by `tests/TurboPatch.Core.Tests`
(xUnit, runs on any OS):

```powershell
dotnet test tests\TurboPatch.Core.Tests
```

`build.ps1 -Release` runs them first and stops if any fail. The manual checks for a Windows PC are in
[docs/TESTING.md](TESTING.md).

## Make a ready-to-share copy

This makes one zip that anyone with Windows 10 or 11 (x64) can unzip and run, with nothing else to
install. Nothing is uploaded or published anywhere; you decide who gets the file.

1. Install the **.NET 8 SDK** once (link above) on the PC where you build.
2. Double-click **`release.cmd`** (or run `powershell -ExecutionPolicy Bypass -File .\build.ps1 -Release`).
   It takes a few minutes the first time.
3. When it's done, the `release` folder opens with:
   - `TurboPatch-<version>-win-x64.zip`: the copy to share. Inside: `TurboPatch.exe` (self-contained,
     .NET included), the `community-configs` folder, `READ-ME-FIRST.txt` (how to start it, the
     SmartScreen warning, where settings live, how to remove it) and `THIRD_PARTY_NOTICES.md`.
   - `TurboPatch-<version>-win-x64.zip.sha256.txt`: its SHA-256 checksum, so whoever gets the zip can
     check it arrived unchanged (`Get-FileHash <zip> -Algorithm SHA256`).
4. Share the zip however you like (a USB stick, a cloud drive link, a chat). The version number comes
   from `<Version>` in `src/TurboPatch.App/TurboPatch.App.csproj`; raise it before making a new copy.

Good to know before sharing:

- The exe isn't code-signed, so Windows SmartScreen may say "Windows protected your PC" the first
  time; *More info → Run anyway*. (A code-signing certificate removes that, but costs money.)
- Some antivirus programs are wary of unsigned apps that ask for administrator rights and inject
  DLLs into games. That's what ReShade installs are, so a false alarm is possible.
- Settings live in the recipient's own `%AppData%\TurboPatch`; nothing of yours is in the zip.
- TurboPatch is free and not for sale; the tools it links to keep their own licenses (see
  `THIRD_PARTY_NOTICES.md`). Add a licence file of your choosing if you want to say how others may
  reuse the source.

## Publish a release (installer and updates)

Installed copies update themselves from this repository's GitHub releases (`AppInfo.GitHubRepo`), using
[Velopack](https://velopack.io). To publish a new version:

1. Raise `<Version>` in `src/TurboPatch.App/TurboPatch.App.csproj` (it must be higher than the last release)
   and add `docs/changes/CHANGES-v<version>.md`; its text becomes the release notes.
2. Either push a tag for it (`git tag v1.4.28` then `git push origin v1.4.28`): the *Release* workflow in
   `.github/workflows/release.yml` tests, builds and publishes it on GitHub by itself. Or, on your PC,
   double-click **`publish-release.cmd`**: it asks for a GitHub token with write access to the repository's
   releases (a fine-grained token with *Contents: Read and write*), then does the same.
3. That's all: every installed copy finds it at its next daily check (or *Check now*), downloads it and
   installs it when TurboPatch closes.

`.\build.ps1 -Installer` (or `release.cmd`) only makes the files, in `release\installer`, without publishing:
the `.msi` installer, the full update package `TurboPatch-<version>-full.nupkg`, a smaller delta package when
the previous release could be downloaded, and `releases.win.json`, the list installed copies read. The `.msi`
can only be made on Windows. Velopack's per-user `Setup.exe` and `Portable.zip` are left out on purpose: they'd
install TurboPatch in a folder other programs can change, and TurboPatch runs as administrator.

Nothing is signed yet, so Windows SmartScreen warns before the installer runs (*More info → Run anyway*).
Updates are still checked: each one must match the SHA-256 in the release's `releases.win.json`.

## First run

1. **Tools** page: install what you want to use (MSI Afterburner and RTSS are the main ones).
2. In **MSI Afterburner**, save profiles in slots 1–5 (e.g. 1 = stock, 2 = undervolt, 3 = overclock).
3. **Mods** page: pick a game, *Install or update* ReShade, then add RenoDX / ReLimiter / BFI
   Presenter. Tick shader collections and press *Download ticked collections*.
4. **Library**: set the *While playing* settings (shared by all games, or *Only this game*), save, then *Play*.
5. **Shaders** page (optional): install SCSKiller from the Tools page, then *Compile all that are ready*
   so games known to stutter build their shaders before you play.
6. **Settings → In game** (optional): pick a suspend shortcut / controller buttons, and turn on
   *Keep this look in every game* for ReShade.
7. Keep TurboPatch running in the tray so profiles apply when you launch games elsewhere.

## How the integrations work

| Integration | Method |
|---|---|
| ReShade | Downloads `ReShade_Setup_<version>_Addon.exe` from reshade.me, extracts ReShade64/32.dll, installs as dxgi.dll / d3d9.dll / opengl32.dll (chosen from the exe's imports) and backs up any DLL it replaces. `ReShade.ini` is pointed at the shared shader folder. If reshade.me can't be reached, pick an installer you downloaded. Vulkan games need the official installer (it registers a system-wide layer). |
| RenoDX | Parses the official wiki mod table, ranks matches by name, installs the `.addon64/.addon32` for the game's bitness. Nexus-only mods open their page instead. |
| ReLimiter, BFI Presenter | Latest GitHub release, correct bitness, next to ReShade. |
| DLSS | Finds `nvngx_dlss*.dll`, shows versions, replaces with a file you pick (original kept as `.tpbak`). Super Resolution (`nvngx_dlss.dll`) and Ray Reconstruction (`nvngx_dlssd.dll`) can update straight from NVIDIA's DLSS SDK repository on GitHub (`lib/Windows_x86_64/rel`; the version shown is its latest release); Frame Generation isn't published there, so it still takes a file you pick. |
| DLSS 5 | Two community routes, picked per game. **renodx-dlss** (64-bit DX9/11/12 games that already have DLSS): the add-on goes next to ReShade, other DLSS-hooking add-ons are switched off (renamed `.off`). **DLSS5-Feeder** (everything else): TurboPatch downloads the feeder's own `tools/Install-DLSS5Feeder.ps1` from its GitHub repository and runs it in a visible PowerShell window with the game folder, your chosen neural add-on (RenoDX, OptiScaler DLSS-NR or Deep Fried Chicken) and your Discord-only files passed in; the installer does the rest and keeps its own backups. Files shared only on Discord are added once and kept in `%LocalAppData%\TurboPatch\dlss5`. Needs an NVIDIA RTX card. |
| Shaders (SCSKiller) | SCSKiller's command-line tool (`%LocalAppData%\SCSKiller.App\cli\scskiller.exe`): `scan` for the game list, `cache get` for the cache size, `compile <id>` / `compile --all-ready --idle` with its output streamed to the page; Stop sends Ctrl+C so it finishes what's in flight. Recordings and offline sessions are done in SCSKiller's own window. |
| Update checks | GitHub's latest release for the tools that publish there (Fan Control, DS4Windows, HidHide, x360ce, SCSKiller, Monarch, BFI Presenter, RHI, DLSS5-Feeder) and for the ReShade add-ons (ReLimiter, BFI Presenter); the winget package list for MSI Afterburner and RTSS; reshade.me for ReShade; for RenoDX mods (which have no version numbers), the date of each mod's download against the copy in the game; NVIDIA's DLSS repository; the shader repositories' latest commit. Installed versions come from the exe's file version or the installed DLLs in your games. Results are cached; nothing is installed without you. |
| Settings for all games | One shared *while playing* profile (`allGames` in `profiles.json`) used by every game whose own profile isn't switched on. Older profiles that already had settings keep them. The shared RTSS frame limit is written to each game that uses it (RTSS keeps limits per exe), and again when such a game is started with Play. |
| Suspend / resume | Only for library games without anti-cheat. The game's windows are minimized first (`ShowWindowAsync`, so a busy game can't block TurboPatch) and given a moment to pause and leave exclusive full screen; then every process running from the game's folder is frozen with `NtSuspendProcess` (all threads at once, as Process Explorer does) and later woken with `NtResumeProcess`, and the main window is brought back. The frozen processes are written to `%LocalAppData%\TurboPatch\suspended.json` and woken when TurboPatch exits or starts after a crash. Suspended time doesn't count as playtime. Keyboard: a system-wide `RegisterHotKey` shortcut (default Ctrl+Alt+P). Controller: XInput, polled 20 times a second only while a game runs; the buttons must be held together for the set time (default LT + RT + left stick click for 1 s). |
| Achievements | Steam games only. From Steam's own stats cache: `appcache\stats\UserGameStatsSchema_<app>.bin` (the achievement list; binary KeyValues) and the newest `UserGameStats_<account>_<app>.bin` (one bit per unlocked achievement). With a Steam Web API key: `ISteamUserStats/GetPlayerAchievements` for your SteamID64 (found in `config\loginusers.vdf`, or typed in). Other stores don't keep achievements in readable files. |
| ReShade look | Written to each game's `ReShade.ini`, `[STYLE]`: `StyleIndex` (0 dark, 1 light, 2 default, 4 custom), `Alpha`, the `*Rounding` values, `Font`, `FontSize`, `ColFPSText`, `FPSScale`, and for your own colors every Dear ImGui color (`Text`, `WindowBg`, `Button`…) worked out from background, text and accent. Applied when ReShade is installed and each time Play starts a game with ReShade; *Back to ReShade's own look* removes those keys again. |
| Launch card | A small window that can't take focus or be clicked (`WS_EX_NOACTIVATE`, `WS_EX_TRANSPARENT`, not in Alt+Tab). It fades out a few seconds after the game is running, or after 30 s. |
| Sounds | 16-bit WAVs built into the app, scaled to the volume in memory and played with `PlaySound` (no other audio settings are touched). |
| MSI Afterburner | `MSIAfterburner.exe -ProfileN`. |
| RTSS | Frame limit via the RTSSHooks64.dll profile API (`FramerateLimit`), falling back to editing `Profiles\<game>.exe.cfg`. Live FPS from the `RTSSSharedMemoryV2` shared memory. |
| Monitors / HDR | Windows `QueryDisplayConfig` / `SetDisplayConfig` and `DisplayConfigSetDeviceInfo` (advanced color). |
| Brightness | External monitors over DDC/CI (`dxva2.dll`, VCP code 0x10, the same channel as the monitor's own buttons); a laptop's built-in screen through Windows' WMI brightness (`WmiMonitorBrightnessMethods`). Game profiles restore the previous brightness when the game closes. |
| Power plans | `powrprof.dll` (works on non-English Windows). |
| HidHide | `HidHideCLI.exe` (`--cloak-on/off`, `--app-reg`, `--dev-gaming`, `--dev-hide`). |
| Controllers | XInput (`xinput1_4.dll`). |
| Community settings | `index.json`, `tiers.json` and one JSON file per game from each source (GitHub links are read from `raw.githubusercontent.com`, cached; folders read directly); INI / JSON / registry (HKCU only) writers with timestamped backups. *My presets* are kept as the same files in `%AppData%\TurboPatch\my-presets`. |
| Store icons | Each badge uses the icon of the store's own launcher installed on your PC (Steam, Epic, GOG Galaxy, EA app, Ubisoft Connect, Battle.net, Xbox app, Rockstar Games Launcher), turned into a white silhouette. To use your own, put a PNG or ICO in `%AppData%\TurboPatch\store-icons` named `steam`, `epic`, `gog`, `ea`, `ubisoft`, `battlenet`, `xbox`, `rockstar` or `folder`. Without either, the badge shows the store's name. |
| Store scanning | Steam `libraryfolders.vdf` + `appmanifest_*.acf`; Epic `.item` manifests; GOG and Ubisoft registry keys; EA / Battle.net / Rockstar uninstall entries; Xbox `.GamingRoot` + `MicrosoftGame.config` / `appxmanifest.xml` (launched as `shell:AppsFolder\<family>!<app>`). |
| Folder scanning | Every subfolder holding a plausible game exe (also `bin\x64`, Unreal `Binaries\Win64` layouts) becomes a game; folders that only group games are searched up to three levels deep. Repack/scene tags and versions are cleaned from names. Removed folder games are remembered and not re-added. |
| Artwork | Steam's local `librarycache` (covers, headers, hero art and `logo.png`), Steam's store API and CDN, or the SteamGridDB v2 API with your key (grids, heroes and logos). The banner view fetches hero art and logos for games that don't have them yet, a few at a time and never while a game runs. |
| Save folders | Ludusavi's `manifest.yaml` (downloaded weekly, ~18 MB), matched by Steam/GOG id, name or install folder; then common save places by name. Backups are zips with an index so they can be restored to the same folders. |
| Launch options | Started through a temporary shortcut so games still run as your normal user; Steam games get them through `steam://run`. |

## Files it creates

- `%AppData%\TurboPatch` — settings, themes, game library and per-game profiles (JSON); background pictures you pick; your own community presets (`my-presets`); your own store icons (`store-icons`, optional).
- `%LocalAppData%\TurboPatch` — downloads, artwork (covers, banners, logos), the save-location list, save backups (`SaveBackups`), shared ReShade shaders, DLSS 5 files you added (`dlss5`), logs, and `suspended.json` while a game is suspended.
- In game folders — only what you install, plus `.tpbak` backups of anything replaced, and the `[STYLE]` keys in `ReShade.ini` if you keep a ReShade look.
- `%LocalAppData%\TurboPatch\CommunityBackups` — backups of the settings files and registry values a community preset changed (the last 20 per file); *Restore* puts them back. Nothing is written next to the game's own settings files.
- `%LocalAppData%\TurboPatch\placed-files.json` — which file TurboPatch placed in each game folder, so a game update that replaces it doesn't make an old `.tpbak` come back later.
- Next to each settings file: `.bak`, the previous good copy. A file that can't be read is kept as `.corrupt-<date>` and the `.bak` is used instead; TurboPatch says so at start.
- The Steam and SteamGridDB keys are saved encrypted for your Windows account (they can't be read on another PC or by another user).

## Limitations

- EA app, Battle.net and Rockstar games are found through Windows' installed-apps list and started by their exe (their launcher takes over). Xbox / Game Pass games are started through Windows; they can't take launch options, and their folders may not accept mods.
- Saves kept only in the cloud or in the registry can't be opened as a folder (the Save files section says so).
- SteamGridDB is optional; without a key, art comes from Steam, which covers most games.
- Turning a monitor back on restores the saved layout or switches to Extend mode; after a driver update a saved layout may need saving again.
- CPU tuning is done in AMD/Intel's own tools; TurboPatch opens them.
- One automated game session at a time.
- DLSS 5 add-ons are community projects; some pieces are shared only on their Discord servers, so they have to be downloaded there once. Use them offline only in games with anti-cheat.
- On a game with anti-cheat, ReShade, RenoDX, add-ons, DLSS 5 and DLSS swaps are refused until you type the confirmation once for that game (you play it offline). Detection goes by the anti-cheat's files, so an unusual one can still be missed.
- SCSKiller compiles DirectX 11/12 games on NVIDIA and AMD; some games need a short recording or an offline session in SCSKiller's own window first.
- Suspending works on games without anti-cheat; online games drop their connection while frozen, and a few games may stutter for a moment after waking. Some keyboards' AltGr counts as Ctrl+Alt, so pick a shortcut that doesn't clash with a character you type.
- Achievements are shown for Steam games only; Steam's own files have them once you've run the game with Steam.
- The window keeping its glass while in the background relies on how Windows draws a window's frame; if a Windows update changes that, frosted glass may turn solid in the background again (blurred and clear glass are unaffected).
- Brightness needs DDC/CI switched on in the monitor's own menu (most monitors have it on; many TVs and some docks or KVMs don't pass it through).

## Project layout

```
src/TurboPatch.Core   all logic and view models (no UI references; builds on any OS)
  Localization/       L.cs (translation lookup, plurals) and Strings/*.json (translations)
src/TurboPatch.App    WPF user interface, tray icon, dialogs
tests/TurboPatch.Core.Tests   unit tests for the Core library (xUnit)
community-configs/   template for the community settings repository
docs/changes/        what changed in each version (CHANGES-v*.md)
docs/TESTING.md      automated tests and the manual checklist for Windows
tools/l10n/          string extraction and translation checks
tools/release/       the read-me that goes into the ready-to-share zip
tools/make_sounds.py makes the three sound effect sets (Assets/Sounds)
build.cmd, release.cmd, build.ps1   building, and the ready-to-share zip
```

See [`THIRD_PARTY_NOTICES.md`](../THIRD_PARTY_NOTICES.md) for the projects this builds on.

# How TurboPatch works

Technical notes for people who want to build TurboPatch, check what it does to their PC, or
contribute. For what TurboPatch is and how to use it, see the [README](../README.md).

## Build and run

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

## Translations

Translations live in `src/TurboPatch.Core/Localization/Strings/<language>.<n>.json` (embedded in the
app). The key is the English text; a value is either the translation or, for counted text, an object
with the language's plural forms (`zero`, `one`, `two`, `few`, `many`, `other`). Anything missing
falls back to English. To fix a translation, edit the JSON and rebuild. To check all languages after
changing UI text, run:

```
python tools/l10n/extract.py             # lists every translatable English string (tools/l10n/keys.json)
python tools/l10n/check_translations.py  # coverage, {0} placeholders and plural forms per language
```

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
| Suspend / resume | Only for library games without anti-cheat. The game's windows are minimized first (`ShowWindowAsync`, so a busy game can't block TurboPatch) and given a moment to pause and leave exclusive full screen; then every process running from the game's folder is frozen with `NtSuspendProcess` (all threads at once, as Process Explorer does) and later woken with `NtResumeProcess`, and the main window is brought back. The frozen processes are written to `%LocalAppData%\TurboPatch\suspended.json` and woken when TurboPatch exits or starts after a crash. Suspended time doesn't count as playtime. Keyboard: a system-wide `RegisterHotKey` shortcut (default Ctrl+Alt+P). Controller: XInput, polled 20 times a second only while a game runs; the buttons must be held together for the set time (default LB + RB + Menu for 1 s). |
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

## Limitations

- EA app, Battle.net and Rockstar games are found through Windows' installed-apps list and started by their exe (their launcher takes over). Xbox / Game Pass games are started through Windows; they can't take launch options, and their folders may not accept mods.
- Saves kept only in the cloud or in the registry can't be opened as a folder (the Save files section says so).
- SteamGridDB is optional; without a key, art comes from Steam, which covers most games.
- Turning a monitor back on restores the saved layout or switches to Extend mode; after a driver update a saved layout may need saving again.
- CPU tuning is done in AMD/Intel's own tools; TurboPatch opens them.
- One automated game session at a time.
- DLSS 5 add-ons are community projects; some pieces are shared only on their Discord servers, so they have to be downloaded there once. Use them offline only in games with anti-cheat.
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
community-configs/   template for the community settings repository
tools/l10n/          string extraction and translation checks
tools/release/       the read-me that goes into the ready-to-share zip
tools/make_sounds.py makes the three sound effect sets (Assets/Sounds)
build.cmd, release.cmd, build.ps1   building, and the ready-to-share zip
```

See [`THIRD_PARTY_NOTICES.md`](../THIRD_PARTY_NOTICES.md) for the projects this builds on.

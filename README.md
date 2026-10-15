[README.md](https://github.com/user-attachments/files/33491944/README.md)
# vShell  (v0.10)

A standalone Windows 11 bar/shell, ported in spirit from **SharpE's SharpBar** (SrcForger/SharpEnviro). It is a
C#/.NET 8 + WPF rewrite - the original is Delphi 2007 code tied to SharpE's skin engine and services.
No NuGet packages needed. GPL-3.0 (derived from SharpEnviro's design).



## Modules (set individually per bar)

| Module | What it does |
|---|---|
| **Start menu** | A Start button that opens a themed menu of every installed program (Start Menu shortcuts plus Store apps) in A-Z sections, with a search box (type to filter, Up/Down + Enter to launch). A left strip has your user/Documents/Downloads/Pictures folders, Settings and a **Power** button (lock, sleep, sign out, restart, shut down). A lone press of the **Windows key** opens it (Win+E, Win+R etc. still work). The button shows the vShell mark - three dots in the Main Accent (or a colour you pick), Secondary Accent and text colour, or a **custom icon** (image, .ico or a program). |
| **Application launcher** | Individual shortcuts and **groups**; a group opens a themed popup menu of its shortcuts. Drop files onto it on the bar to add them, or use *Settings -> Edit shortcuts and groups…*. Icon size, separate show-names switches for shortcuts and for groups, and a **custom icon** (image, .ico or a program) for any shortcut or group. |
| **Taskbar** | Open windows, combined per app (always / when full / never) as icons, icon + name or icon + title; live window previews on hover; click an app with several windows to pick one; pinned apps (shared by all taskbars); progress, badges and attention flashing; right-click menu (new window, pin, close all). Optional "only this monitor's windows". |
| **CPU / Memory / GPU monitor** | Text plus **Meter**, **Bars** (bar graph) or **Line** (line graph) styles; configurable graph width, graph height (% of the bar, always vertically centred), colour, show/hide text. Memory can show used/total GB; GPU can show VRAM. GPU works on any vendor (Windows performance counters), pick the adapter if you have several. Optional **temperature** (see below). |
| **HWiNFO sensor** | Shows any value HWiNFO publishes (temperatures, fans, voltages, clocks, power ...) as text, meter, bar graph or line graph, with its own title, unit, decimals and graph range. See *HWiNFO and temperatures*. |
| **Clock** | Time and/or date. 12-hour (AM/PM) or 24-hour, optional seconds, date format (short / medium / long / ISO) and six layouts: time only, time and date on one line, time above date, date above time, large time above small date, date only. Defaults to your Windows 12/24-hour preference. |
| **System tray** | Icons drawn on the bar, in shell mode and (taking over Explorer's tray registration, like Cairo) alongside Explorer. Icons are grouped behind an arrow; click it for a popup. **Drag an icon out of the popup onto the bar to pin it** (always visible); drag a pinned icon onto the arrow to hide it again. Grouping can be switched off. |
| **Network speed** | Download and upload speed (MB/s or Mbit/s) with an optional meter / bars / line graph of the download, optional Wi-Fi name and signal. Only adapters with a gateway are counted, so VPNs and virtual switches are not double-counted. |
| **Disk space / activity** | Used space of a drive (as % or used/total GB) with a meter, or live disk busy % with read/write speed; either can be on two lines. |
| **Battery** | Charge %, a + while charging, time left in the tooltip. Hides itself on a PC without a battery (switchable). |
| **Volume** | Master volume of the default speakers with a speaker icon (changes with the level, crossed out when muted), as text and/or a plain meter (adjustable width). Scroll over it to change, click for Mute and a list of output devices to switch between, plus a link to Sound settings. |
| **Uptime** | How long Windows has been running. |
| **Top processes** | The busiest program by CPU or memory (processes of one program are added together). Show 1-5 programs on the bar or widget (side by side, or as a list with its own text size and line spacing); the tooltip lists more, click opens Task Manager. |
| **Text label** | A piece of text (bold, size, colour) - headings and notes for widgets. |
| **Home Assistant entities** | Any entities you choose, with their values; click a light, switch, scene, script, button, lock, cover or automation to operate it. Pick them from a list fetched from Home Assistant. Connection details on the Integrations page of Settings (address + long-lived token, stored encrypted for your Windows account). |
| **Weather** | Icon and temperature (optionally the condition and today's high / low), details on hover, a 7-day forecast on click. From Open-Meteo (free, no account - search for your town) or a Home Assistant weather entity. |
| **Now playing** | Album art, title and artist of whatever Windows' media controls show (Spotify, browsers, Plex ...), with previous / play-pause / next buttons, scroll to change track, and a bigger card on click. |
| **Power flow** (widgets) | Solar, grid, battery and home as circles joined by lines with moving dots showing which way the power flows (faster for more power); grid import / export, battery charge % and charging / discharging, and a ring round Home showing how much comes from solar, battery and grid. From Home Assistant power sensors (W or kW). |
| **Proxmox VE** | Your Proxmox cluster: nodes (CPU and memory, as text or small meters), guests (VMs and containers, running count on a bar or a list in a widget) or storage (how full each pool is). On a bar, click for the whole cluster; click a guest for Start / Shut down / Reboot / Stop (asks first). Connection on the Integrations page: one or more node addresses and an API token, secret stored encrypted. |
| **Service status** | A coloured dot per service (green up, yellow slow, red down) checked in the background by web address, TCP port or ping; click a web address to open it. |
| **Spacer** | Flexible gap (pushes the modules after it to the right) or a fixed-width gap. |

## Using the bars

* **Move a bar:** drag it by any empty area. Drop on the top or bottom half of any monitor. With *Full width* off the bar
  sits **exactly where you drop it along the edge** (no snapping to left/centre/right) and is remembered per bar.
* **Reorder modules:** **Ctrl+drag** a module left/right within its bar (or use *Move left / Move right* in Settings).
* **Per-bar settings:** *Settings -> Bars* - pick a bar, set its height / full-width, add, remove and configure its own modules.
  *Add bar* creates a bar with just a taskbar for its monitor; add the rest in Settings.
* **Theme colours** (shared by all bars): colours with picker / `#AARRGGBB`, opacity, font family, built-in presets and your own
  presets (*Save as preset…* stores the current colours + font; *Delete* removes a saved one).
* **Per bar:** height, full width, **font size, corner radius, edge margin**, and a corner mode: round all four corners, or only the
  two that do not touch the screen edge (a top bar rounds its bottom corners, a bottom bar its top corners).
* Right-click an empty part of a bar: Settings, add/remove bar, Task Manager, Run, File Explorer, Exit.

Settings live in `%APPDATA%\vShell\settings.json` (old v0.1 files are migrated automatically).
Log: `%APPDATA%\vShell\vshell.log`.

## Widgets

*Settings -> Widgets.* A widget is a box on the desktop that holds one or more modules - **add as many widgets as you like**, one per
module or several modules grouped in one box. Available modules: Start menu, Application launcher, CPU / Memory / GPU monitor,
HWiNFO sensor and Clock (the taskbar, tray and spacer only make sense on a bar).

* **Move:** drag a widget by any empty part (or by a text-only module such as the clock); it stays where you drop it, per monitor. Right-click
  a widget for *Widget settings*, *Lock / Unlock position* and *Hide this widget*.
* **Look (per widget):** stack the modules vertically or side by side, module height (what the bar height is to a bar: clocks and graphs size
  themselves from it), padding, space between modules, font size, **corner radius**, background opacity, border and shadow on/off.
  Colours and the font family come from the Appearance page, shared with the bars.
* **Layer:** by default a widget sits on the desktop behind your windows; tick *Keep above other windows* to float it. *Lock position* stops dragging.
* Works alongside Explorer and in shell mode.

## HWiNFO and temperatures

Windows has no reliable built-in CPU or memory temperature, so those come from **HWiNFO** (the same route Rainmeter uses):

1. In HWiNFO open the **Sensors** window, then its settings (gear) -> **HWiNFO Gadget** tab -> tick **Enable reporting to Gadget**.
   (Do not need Shared Memory.) Needs HWiNFO 7.02 or newer; it must be running.
2. Right-click each sensor reading you want in the Sensors window -> **Report value in Gadget**.
3. In vShell: add an **HWiNFO sensor** module and pick the reading in the list (Refresh re-reads it), or tick
   **Show temperature** on a CPU / Memory / GPU module. Leave the source on *(automatic)* or choose a specific reading.

Automatic temperature: GPU on NVIDIA cards is read straight from the driver (no HWiNFO needed); everything else looks for the
usual HWiNFO readings (CPU Package / Tctl-Tdie, GPU Temperature, DIMM) and shows `n/a` if none is being reported.
Values are shown in whatever unit HWiNFO uses.

## Startup apps

*Settings -> Startup* lists everything Windows starts at sign-in (registry Run keys and the Startup folders). Select entries to
**Enable**, **Disable** or **Remove** them, or **Add** a program. Enable/Disable use the same per-user switch as Task Manager's
Startup tab, so it applies with or without vShell. When vShell is the shell it launches the enabled entries itself
(untick *Start these apps…* to stop that). Removing "all users" entries needs administrator rights; disabling them does not.

## Build

Requires the .NET 8 SDK on Windows: double-click **`build.cmd`** (self-contained `dist\vShell.exe`), or
`.\build.ps1 [-SelfContained]`, or push to GitHub and use the included Actions workflow.

## Runs alongside Explorer
vShell registers its bars as app bars next to Explorer and hides the Windows taskbar. The tray module still works: like Cairo Desktop,
vShell puts its own invisible `Shell_TrayWnd` window in front of Explorer's, so apps send their notification icons to vShell; everything
else (app bars, taskbar queries) is forwarded to Explorer. Panic button: `vShell.exe --restore-taskbar` brings the taskbar back.
From 0.20.1 there is no option to make vShell the Windows shell; if an older version was set as your shell, vShell undoes that at start-up
(Explorer is the shell again from the next sign-in), and `vShell.exe --restore-shell` / `scripts\restore-explorer.ps1` still do it by hand.

## Known gaps
No taskbar grouping or thumbnails, no per-module drag between bars or widgets. The Home Assistant modules use the REST API, so values refresh every few seconds rather than instantly. Wi-Fi details use `netsh`, so they depend on Windows' English output. The Volume module's output-device switch uses an undocumented-but-stable Windows interface. The Start menu has no pinned tiles, recent files or jump lists, and does not show Windows search results (files, web).
GPU memory shows VRAM *in use* only (no total).


## Theming (v0.6)
Theme tab: solid or gradient background (Background to a Gradient colour, with an angle), a Secondary Accent colour, Main Accent / background colours
taken from the wallpaper, and export / import of whole themes (`*.vstheme.json`). Every module has a setting for three large dots
(Main Accent, Secondary Accent and Text colour) shown after it as a separator.

## Taskbar & tray internals (v0.8, after Cairo's ManagedShell)
* The task list is driven by Windows' shell hook (window created / destroyed / activated / title changed / flashing / monitor changed)
  and cloak events, with a slow poll as a safety net.
* Buttons flash when an app asks for attention, show download/copy **progress** and **overlay badges** (ITaskbarList - vShell's
  Shell_TrayWnd carries the `TaskbandHWND` property, so apps' ITaskbarList calls arrive at vShell), and Store apps get their package icon.
* Full-screen detection follows ManagedShell: client-area size for framed windows, Windows' own full-screen notices, cloaked /
  click-through / "non-rude" windows ignored, and a full-screen app stays full screen while you work on another monitor.
* Tray **balloon notifications** are shown in the bar's theme (Settings -> System to turn off).
* Shell mode starts Windows' own Network / Power / Safely Remove Hardware tray icons.
* Windows 11: vShell's windows hide from the taskbar via their hidden owner instead of the tool-window style, so they get DPI change
  messages and scale correctly on mixed-scaling monitors.

## The Secondary Accent colour (v0.9)
Secondary Accent is the theme's "look at this / the other thing" colour:
* the second series of a graph (network upload),
* warnings: every graph module (CPU, memory, GPU, disk, network, battery, HWiNFO sensors, Home Assistant entities) can turn its graph
  and text Secondary Accent past a threshold you set - above it, or below it (battery),
* taskbar buttons that ask for attention, and download / copy progress,
* optional clock seconds / separators / date, and the Start menu's letter headings and search matches,
* one of the three separator dots.
Module colours, the bar outline and the widget border can be set to the theme slots **Main Accent / Secondary Accent / Text** (stored as `@main`,
`@secondary`, `@text`; the old `@accent` / `@spare` are still read) so they follow the theme; a hex colour stays fixed. Built-in presets now include a Secondary Accent and gradient colour each,
plus Cyberpunk, Neon 2077, Synthwave '84, Matrix, Dracula, Tokyo Night, Gruvbox Dark, Rose Pine, Everforest, Kanagawa, Oceanic,
Blood Moon and AMOLED Black.


## The settings window (v0.10)
Rebuilt in a Windows 11 style and coloured from your own vShell theme (dark title bar on dark themes):
* a **sidebar** of pages - Appearance, each bar, each widget, Desktop, Startup apps, Home Assistant, System, About - with
  "+ Add bar" / "+ Add widget" right in it;
* **Appearance** shows themes, colour presets, bar styles and widget styles as small picture cards; click one to apply it
  (see *Themes, bar styles and widget styles* below). Save as theme / Import / Export / Delete theme are the buttons at the top right;
* settings sit in titled **cards**, with on/off **switches**, joined buttons for short choices, and the explanation as a small grey line
  under each setting;
* a bar's or widget's page starts with a **live preview** of the real bar / widget;
* **Edit modules** opens the module editor: the modules as chips in their real order (click to edit, **drag to reorder**), a gallery to
  add new ones grouped by kind with a filter box, and the selected module's settings in folding sections (Graph, Warning, Temperature ...).
  New modules go in after the one selected.
If the window's styles cannot load for any reason it falls back to a plain light look (noted in the log); everything still works.

## Wallpaper Theme (v0.10.2)
Appearance -> Colours -> **Wallpaper Theme - Use colours from the main monitor wallpaper** builds the whole theme from the picture on
your main monitor (its per-monitor wallpaper, otherwise the Windows wallpaper):
* the picture is grouped into its main colours (k-means on a small copy; the same picture always gives the same theme);
* **Background** = the most common colour, nudged a little darker (dark pictures) or lighter (light pictures); mid-tones are pushed
  further so text stays readable. **Gradient** = another shade of it (lighter on dark themes, darker on light ones);
* **Main Accent** = the 2nd colour, **Secondary Accent** = the 3rd. Greys, black and white are skipped as accents; a picture without
  enough colours gets accents made from the hues it has. Both are lightened / darkened until they stand out from the background (3:1);
* **Text** = near-white or near-black tinted with the background hue, at least 4.5:1 contrast with the background and gradient.
Your background opacity and gradient style still apply, and your own colours are kept (greyed out) for when it is off. The theme follows
wallpaper changes. A preview card shows at the top of Appearance with **Save as preset…**, which stores the colours it worked out as a
normal preset. Picking a preset turns the Wallpaper Theme off. Older "accent from the wallpaper" / "tint the background" settings turn
it on.

## Reserve window space (v0.10.5)
Per bar (Settings -> bar -> Size), on by default: the bar stays on top of everything and keeps its strip of the screen, so maximised
windows stop at it. Off: the bar acts like a widget - it sits on the desktop behind your windows and reserves nothing, so windows can use
the whole screen and cover it.

## Logo, icon and splash (v0.12)
The vShell mark is three dots arranged as a v - the same Main Accent / Secondary Accent / Text trio as the separator dots - so on the
bar it always matches the theme. It is the default Start button icon, the exe / window icon (in the default Mocha colours on a dark
tile: `vshell.ico`), and the splash card shown while vShell starts (Settings -> System -> "Show the splash screen while vShell starts").

## Updates

vShell checks https://github.com/version-au/vshell-releases for new versions (a minute after start-up, then daily; Settings > System > Updates).
Publishing a version: run `build.cmd`, then on GitHub create a release in that repo tagged `v` + the version in `vShell.csproj` (e.g. `v0.17.1`),
attach `dist\vShell.exe` **and** `dist\vShell.exe.sha256`, and publish (tick "Set as a pre-release" for test builds).
The installer checks the SHA-256, swaps the exe in place (same path, so shell mode and the startup entry keep working), restarts,
and puts the previous version back if the new one doesn't start.

## Themes, bar styles and widget styles (v0.20.0)
Appearance starts with **Theme**: a theme is colours + a bar style + a widget style, applied in one click. 19 built-in themes (one for each colour preset), plus your own
(*Save as theme…* - choose to include colours, bar style and/or widget style; what a theme leaves out is left as it is). Export / Import
write and read the whole theme (`*.vstheme.json`, version 2; older files still import as colour presets).

Every bar has a **layout**, worked out from its own settings and picked at the top of its page:
* **Classic** - full width, with an outline (corners rounded or not);
* **Minimal** - full width, no outline;
* **Floating** - only as wide as its modules, away from the screen edge;
* **Dock** - only as wide as its modules, against the screen edge.

A **bar style** (Soft, Sharp, Round, Slim, Bold, Hairline, Neon, Ghost, Retro or your own) has a look for each layout - height, corner radius, round all corners,
gap from the edge, outline thickness / opacity / colour - and each bar takes the look for its layout, so one theme can have, say, a Classic
bar at the bottom and a Floating bar at the top. A **widget style** (Soft card, Outlined, Borderless glass, Sharp, Bubble, Neon, Retro or your own) sets
corners, border, shadow, padding and spacing of every widget.
You shape a bar or widget on its own page; **Save Bar Style** / **Save Widget Style** there keep that look as a style (a bar's look
becomes the look for its layout) for themes.

Each bar and widget has **Follow the bar style / Follow the widget style**. Changing a shape setting on its own page turns that off, so
styles and themes leave it alone; turn it back on (or *Make every bar / widget follow the style*) to take the style again. Upgrading keeps
every bar and widget as it was: the style is made from your current bars / widgets, and any that look different keep their own look.

## Background blur (v0.20.1)
Appearance > Background > Background blur: **Blur** or **Frosted**. vShell draws your desktop wallpaper behind each bar and widget, blurred,
under the theme colour (the background opacity decides how much shows through) and inside the bar's / widget's own rounded shape, so the
corners stay smooth and widgets keep their shadow. Frosted is a little lighter with a fine grain, like Windows' acrylic. It follows wallpaper
changes (Windows' wallpaper with its Fill / Fit / Stretch / Center / Tile / Span setting, or vShell's per-monitor pictures). It shows the
wallpaper, not windows: a widget kept above other windows shows the blurred wallpaper, not the app behind it.

## Dock animations (v0.21.0)
On any bar (from 0.21.3; Dock only in 0.21.0-0.21.2), an icon-only Application launcher and Taskbar can **Lift**, **Glow** (strength and
size adjustable), **Magnify** (macOS-style, 110-250 %; Lift or Magnify, not both) and **Bounce** when an app starts (module settings > Icon
animations; all off by default). The bar's window has transparent room above it for the grown icons; clicks go through it. A Dock can also be kept centred on its monitor (bar page, or the bar's right-click menu).

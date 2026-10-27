[Download the updated demo ZIP](https://github.com/mexiscool/horizon_web/raw/refs/heads/webgpu-demo-download/downloads/horizon-webgpu-demo.zip)

Prepared by OpenAI Codex for this experimental browser demo.

# Horizon WebGPU browser demo

1. Extract this ZIP and open a terminal in the `horizon-webgpu-demo` folder.
2. Run `py start_demo.py` on Windows, or `python3 start_demo.py` on macOS/Linux.
3. Open **http://localhost:3000** in a current WebGPU-capable browser, such as Chrome or Edge.

Python 3 is required. The game is already compiled; Rust, Node and Minecraft are
not required to try the original island. Keep the terminal running while playing.
Press Ctrl+C to stop. For a different port, run `start_demo.py --port 8080` and
open http://localhost:8080 instead.

## Load your Minecraft textures and models

Use **Import Minecraft client JAR / resource-pack ZIP** on the menu to select
your own installed Minecraft Java client JAR. The target is **26.3**.
The file is commonly `versions/26.3/26.3.jar` inside your Minecraft directory:

- Windows: `%APPDATA%\.minecraft`
- macOS: `~/Library/Application Support/minecraft`
- Linux: `~/.minecraft`

Import opens a fresh **16 × 16 block test chunk**, clearing current edits. It
contains grass, dirt, stone, sand, oak logs, oak leaves, bottom oak slabs, glass
and a still-water pool. The browser uses Horizon's model decoder, block-state
selection, parent/texture resolution, model baker, quad lighting and mip generator.

After importing a complete base, select another resource-pack ZIP to apply its
overrides. A texture-only pack requires that base. A failed import keeps the
previous assets and world. Reloading the page clears imported assets; select your
files again. **Files are read in your browser, never uploaded or bundled.**

This targets the listed block states, a uniform plains biome and full daylight.
It is a porting test, not a full native-client replacement. General world loading,
all block states, moving fluids, mobs, crafting, persistent saves and multiplayer
are not implemented. Imported models use shared native cardinal shading and AO;
the procedural island's enhanced sunlight effects are a separate demo mode.

## Controls

WASD/arrows move; mouse looks; Space jumps; Left Shift sprints. Left/right click
mine/place. Keys 1–9 or the wheel select grass, stone, sand, oak, leaves, slab,
glass, water and dirt. F toggles flight; Space/Left Ctrl fly up/down; R respawns;
Esc pauses and releases the mouse. Scene switching and import reset edits.

The original project license is in `LICENSE.txt`; third-party notices and font
licenses are included. This archive contains no Minecraft JARs or assets.

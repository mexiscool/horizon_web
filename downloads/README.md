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
It is a porting test, not a full native-client replacement. Moving fluids, mobs, crafting and persistent saves are not implemented.
The offline-server connection described below is an early client port. Imported models use shared native cardinal shading and AO;
the procedural island's enhanced sunlight effects are a separate demo mode.

## Connect to an offline Java 26.3 server

The server must use **Java 26.3 / protocol 777**, with `online-mode=false` and
`enforce-secure-profile=false`. Restart it after changing those properties.
Use a server you control or whose owner has enabled offline connections.
This preview does not log into Microsoft accounts or accept encryption requests.

Browsers cannot connect directly to Minecraft's TCP port. Run the included
**Rust WebSocket bridge** on your computer. It forwards bytes to one fixed server;
it does not run a Minecraft server or implement any server game logic.

1. Start your existing server, then start the browser demo as described above.
2. Start the bridge in a second terminal. The download includes a Linux x86_64
   executable in `bridge/`:

   ```sh
   chmod +x bridge/horizon-web-bridge-linux-x86_64
   ./bridge/horizon-web-bridge-linux-x86_64 --server 127.0.0.1:25565
   ```

   On Windows/macOS, install Rust using https://rustup.rs, then build and run the
   small standalone bridge project included in the ZIP:

   ```sh
   cd bridge
   cargo run --release -- --server 127.0.0.1:25565
   ```

   The first build requires internet access for the bridge's Rust dependencies.
   Replace the target with your server's hostname/IP and port if it runs elsewhere.
   The bridge listens on `127.0.0.1:25566` by default.
3. Import your **26.3 client JAR** in the browser. Open **Join an offline server**
   and import a matching **`blocks.json`** report or Horizon's prepared **`facts.json`**.
   The wire protocol sends numeric state IDs; this file maps those IDs to local
   block models. It must come from the same version/content as the server.
4. Leave the bridge URL as `ws://localhost:25566`. Set **Server handshake address**
   to your actual server address, choose an offline player name, and click
   **Connect**, then **Enter server** when the spawn chunks arrive.

To generate `blocks.json`, use Java 25 or newer and your own unmodified **26.3
server JAR**. In an empty working directory run:

```sh
java -DbundlerMainClass=net.minecraft.data.Main -jar /path/to/26.3-server.jar --reports --output out
```

Import `out/reports/blocks.json`. This invokes Minecraft's existing data generator;
it does not launch a world or require porting server code. A previously prepared
Horizon resource bundle's `facts.json` is another supported source.

The bridge allows `http://localhost:3000` and `http://127.0.0.1:3000` by default.
For another page port, add `--origin http://localhost:8080` to its command.
`--origin` can be repeated; explicit entries replace the defaults.
The handshake address field does not change the bridge's fixed TCP target.
HTTPS hosting needs a `wss://` reverse proxy; the included local bridge speaks
`ws://`. For self-testing, use the local HTTP launcher.

This step supports compressed offline login, configuration/registries, nearby
chunk streaming and light updates, teleports, basic movement/collision, server
inventory hotbar counts, flight permissions, mining/placement requests, unsigned
chat/commands, respawn and server disconnects. **T** opens chat, **/** opens a
command, and **middle click** requests a creative block pick. Block changes come
from the server. You stay connected when the menu is open.

The client is still incomplete: players/mobs/items are not rendered, full
inventory/container/crafting screens are missing, collision shapes and movement
are simplified, biome tint/day-night lighting is approximate, and flowing fluids,
block-entity/special renderers, audio and server resource-pack downloads are not
ported. Unsupported models show a missing-model marker. The nearby chunk cache
and texture budget are bounded. Start with a small creative world. Automated
coverage uses a protocol regression fixture; real vanilla 26.3 server compatibility
has not yet been validated here because no matching game JAR is installed.

## Controls

WASD/arrows move; mouse looks; Space jumps; Left Shift sprints. Left/right click
mine/place. Keys 1–9 or the wheel select grass, stone, sand, oak, leaves, slab,
glass, water and dirt. F toggles flight; Space/Left Ctrl fly up/down; R respawns;
Esc pauses and releases the mouse. Scene switching and import reset edits.

The original project license is in `LICENSE.txt`; third-party notices and font
licenses are included. This archive contains no Minecraft JARs or assets.

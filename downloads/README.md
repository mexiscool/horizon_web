# Horizon WebGPU browser demo

Prepared by OpenAI Codex for this experimental browser demo.

[Download the prebuilt ZIP](https://github.com/mexiscool/horizon_web/raw/refs/heads/webgpu-demo-download/downloads/horizon-webgpu-demo.zip)

1. Extract `horizon-webgpu-demo.zip` on your computer.
2. Open a terminal in the extracted `horizon-webgpu-demo` folder.
3. Start the server with `py start_demo.py` on Windows, or `python3 start_demo.py` on macOS/Linux.
4. Open **http://localhost:3000** in a current WebGPU-capable browser and click **Play world**.

Python 3 is required. The game is already compiled; Rust, Node, and Minecraft are
not required. Keep the terminal running while playing; press Ctrl+C to stop it.
If port 3000 is occupied, run the server with `--port 8080` and open
http://localhost:8080 instead.

Use WASD to move, the mouse to look, Space to jump, left/right click to mine/place,
1–5 to select a block, F to toggle flight, and Esc to pause. Further instructions
and licenses are inside the ZIP. `SHA256SUMS` contains the archive checksum.

This is a limited, experimental browser slice using Horizon's Rust core and wgpu's
WebGPU backend. It has an original finite island and original procedural materials.
It is not the complete native game: mobs, crafting, persistent saves and multiplayer
are not implemented. Edits last until regeneration or reload.

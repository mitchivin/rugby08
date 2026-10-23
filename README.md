<div align="center">
  <h1>Rugby 08 in the browser</h1>
  <a href="https://mitchivin.github.io/rugby08/"><img src="assets/main-menu.png" width="720" alt="Rugby 08 main menu running in Chrome"></a>
  <p>Play Rugby 08, the 2007 PC rugby game, in your browser. The original Windows game is recompiled to WebAssembly, with online play for up to four people.</p>
  <p><a href="https://mitchivin.github.io/rugby08/"><strong>Play now at mitchivin.github.io/rugby08</strong></a></p>
</div>

## Features

- **The full game in a browser tab.** Menus, Play Now matches, My Rugby, intro videos, crowd and commentary audio.
- **No emulator.** The game's own code runs as WebAssembly. There's no Wine, DOSBox or virtual machine.
- **Online multiplayer.** Up to four players in a party, joined by an invite link, on the same team or against each other.
- **60 fps.** Frames are paced with `requestAnimationFrame`, and rendering runs on its own thread.
- **Controller and keyboard.** Xbox-style controllers work from the start screen, and every action has a keyboard key.
- **Installable app.** Chrome and Edge can install it to the desktop and launch it full screen.
- **Nothing to install or sign up for.** About 168 MB downloads on first start.

## Play

Open [mitchivin.github.io/rugby08](https://mitchivin.github.io/rugby08/) in Chrome or Edge on a desktop computer and press **Play**.

The game downloads about 168 MB on first start. Nothing is installed and no account is needed.

## Play online

1. Press **Play**. When the **Play online** panel appears, pick your region (Australia / Pacific, North America or Europe) and press **Play online**. **Play offline** skips this.
2. You are now hosting a party. Press **Copy invite link** and send it to up to three friends.
3. Each friend opens the link and presses **Play online**. Their game catches up to yours behind the **Joining the party** screen, then they are in.
4. On **Team Select**, each player moves their controller icon to a side. Players on the same side play together.

Every game in the party runs the same simulation in lockstep and the games compare their state as they go, so everyone sees the same match. Players connect to each other directly where they can and through a relay where they can't. If the connection drops, your game carries on offline.

## Controls

A game controller is used when one is connected. Press a button on it once so the browser makes it available. It works from the start screen on: **A** presses **Play**, and on the **Play online** panel the d-pad moves between the region and the buttons, **A** presses the selected button and **B** plays offline.

| Action | Controller |
| :--- | :--- |
| Move, menu navigation | Left stick or d-pad |
| Accept, offload, dive, score try, punt | **A** |
| Pass left / right (hold for a long pass) | **LB** / **RB** |
| Sprint | **RT** |
| Change player | **LT** |
| Grubber kick | **Y** |
| Up and under, call a mark | **X** |
| Drop goal, jump to catch | **B** |
| Sidestep, hand-off, shoulder charge | Right stick |
| Pause | **Start** |

If the controller is unplugged during a match the computer takes over your player until you plug it back in. One controller per browser.

On the keyboard:

| Action | Key |
| :--- | :--- |
| Move, menu navigation | Arrow keys |
| Accept, offload, dive, score try, punt | **S** or **Enter** |
| Pass left / right (hold for a long pass) | **A** / **D** |
| Sprint | **Space** |
| Change player | **Left Shift** |
| Grubber kick | **W** |
| Up and under, call a mark | **Q** |
| Drop goal, jump to catch | **E** |
| Sidestep, hand-off, shoulder charge | Numpad **4 / 6 / 8 / 2** |
| Pause | **Esc** |
| Start | **Left Ctrl** |

Hold a kick key to build power and steer with the arrows. In scrums, rucks, mauls and line-outs the same keys take on the set-piece actions shown on screen.

## Requirements

- A current version of Chrome or Edge. Other browsers are not tested.
- WebGL 2 and WebAssembly support.
- A keyboard or a game controller.

## How it works

```
Rugby08.exe (x86, 2007) ──static recompilation──▶ C (about 4.2 million lines) ──Emscripten──▶ WebAssembly
Direct3D 8 ──▶ WebGL 2      DirectInput ──▶ Gamepad + keyboard      DirectSound ──▶ Web Audio
```

- **Recompiled game.** Every function in the original Windows executable is translated to C ahead of time, including x87 floating point and jump tables, then compiled to WebAssembly with Emscripten. A small runtime provides the parts of Windows, Direct3D 8, DirectInput and DirectSound the game expects.
- **Shaders.** The game's vertex shaders are translated to GLSL with MojoShader.
- **Renderer.** Direct3D calls are translated to WebGL 2. Rendering runs on its own thread through an offscreen canvas.
- **Game data.** Game files are stored as compressed chunks on Cloudflare R2, fetched as needed and unpacked in a background worker.
- **Online.** A Cloudflare Worker runs the parties: it issues short-lived tickets, relays inputs and connection setup between players, and keeps the match history so late joiners can catch up. Players exchange inputs over WebRTC, with TURN for networks that block direct connections.

## Built with

[pcrecomp](https://github.com/sp00nznet/pcrecomp) and [xboxrecomp](https://github.com/sp00nznet/xboxrecomp) (static recompilation), [d3d8to9](https://github.com/crosire/d3d8to9), [MojoShader](https://github.com/icculus/mojoshader), [d3d9-webgl](https://github.com/LostMyCode/d3d9-webgl), [SDL2](https://www.libsdl.org/), [Emscripten](https://emscripten.org/), [Ghidra](https://ghidra-sre.org/), [Cloudflare Workers and R2](https://developers.cloudflare.com/) and WebRTC.

## Repository

This repository holds the project page, artwork and the GitHub Pages deployment. The source and build pipeline are kept privately.

**Search terms:** Rugby 08 PC, play Rugby 08 in browser, Rugby 08 online, Rugby 08 WebAssembly, rugby game in browser, online rugby game, static recompilation, x86 to WebAssembly, Direct3D 8 to WebGL, PC game port, retro sports game.

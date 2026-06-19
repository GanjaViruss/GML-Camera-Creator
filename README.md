# GML Camera Creator

Build a complete camera system for GameMaker without writing the boilerplate. Pick your options, get one `obj_camera` ready to drop in.

🔗 **[Open the tool »](https://ganjaviruss.github.io/GML-Camera-Creator/)**

Cameras in GameMaker trip a lot of people up — views, viewports, the application surface and the GUI layer all interact, and it's easy to end up with a blurry or stretched mess. This tool generates a clean, complete camera object from a few choices, so you skip the boilerplate and the head-scratching.

---

## What you get

One script with `camera_init()`, `camera_update()` and optional helpers like `camera_shake()`, `camera_set_zoom()` and `camera_set_resolution()`. You paste it into a script asset, then call the functions from an `obj_camera`. The tool shows you exactly which call goes in which event.

---

## Options

**Base resolution & render mode**
Pick the size your game renders at (presets or custom). Choose **pixel art** (surface stays at base size, scaled with no blur — best for pixel games) or **smooth / HD** (surface renders at window size for crisp high-res scaling).

**Follow**
The camera tracks a target object. Options:
- **Smooth follow** — eases toward the target instead of snapping, with adjustable smoothing
- **Deadzone** — the target can move inside a box before the camera starts following
- **Clamp to room** — stops the camera at the room edges

**Extras**
- **Screen shake** — adds `camera_shake(amount, length)`. Call it from anywhere: `with (obj_camera) camera_shake(4, 20);`
- **Zoom** — smooth zoom in/out with a range you set, controlled by mouse wheel, Q/E keys, or code only

**Window & aspect ratio**
Adds `camera_set_resolution(w, h, fullscreen)` for switching between fullscreen and windowed. Choose how the game fits different screens:
- **Keep** — letterbox with black bars, pixels stay square (the safe default)
- **Expand** — wider screens see more of the room, no bars
- **Stretch** — fills the screen but distorts the image

Optional borderless fullscreen instead of exclusive.

---

## GUI scaling

The HUD layer can work three ways:

- **Match base** — GUI uses the base resolution, GameMaker stretches it to fit. Simplest, looks the same everywhere.
- **Custom** — a fixed GUI size you set, stretched to the screen.
- **Scaled** — GUI matches the real screen size and you get a `GUI_SCALE` value to multiply your HUD by. This keeps the HUD crisp (great for pixel art) and the right size on any screen.

With **Scaled**, `GUI_SCALE` works out to `1` at your design size, `2` at double, `0.5` at half. Use it in Draw GUI:

```gml
draw_sprite_ext(spr_heart, 0, x, y, GUI_SCALE, GUI_SCALE, 0, c_white, 1);
draw_text_transformed(x, y, "SCORE", GUI_SCALE, GUI_SCALE, 0);
```

There's also a **user multiplier** — `global.gui_scale_user` (1.0 = normal). Call `gui_scale_increase()` / `gui_scale_decrease()` from an options menu and the whole HUD scales up or down by your chosen step. So someone on a 4K screen who still wants a bigger HUD can just bump it. Save `global.gui_scale_user` with your settings to remember it.

---

## Setup

1. Make a new **Script** asset (e.g. `scr_camera`) and paste the generated script into it.
2. Make an object `obj_camera`, place it in your room (no sprite needed).
3. Put the calls in the events the tool tells you: **Create** → `camera_init()`, **Step** → `camera_update()` (plus the input lines if you enabled zoom).
4. Run the game.

`obj_player` is just a placeholder for whatever the camera follows — use your own object. The generated code is plain GML; open it and change anything.

---

## License

MIT. Free to use, modify and share.

Part of [GML Tools](https://github.com/GanjaViruss/GML-Tools).

*Built by [GanjaViruss](https://github.com/GanjaViruss) with Claude Opus 4.8 & Sonnet 4.6.*

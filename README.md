# Maple Saturation (Hyprland)

Real-time screen saturation, contrast and gamma control for Hyprland through a GLSL screen shader, with a PyQt6 GUI.

Companion project for KDE Plasma: [maple-saturation-plasma](https://github.com/MapleProjects/maple-saturation-plasma).

## How it works

The app writes `~/.config/hypr/shaders/saturation.glsl` and runs `hyprctl reload`. The shader converts sRGB to linear space, scales chroma around Rec. 709 luminance, applies contrast around a 0.5 pivot, then applies a gamma curve. Only output index 0 is processed; every other output is passed through untouched.

Hyprland has to point at the shader in its config, otherwise reloading changes nothing:

```ini
decoration {
    screen_shader = ~/.config/hypr/shaders/saturation.glsl
}
```

If you use the Lua config style, set the same path in your `decoration` block.

## Features

- Saturation 0.00x to 4.00x in linear light, hue-preserving
- Contrast 0.50x to 2.00x with a 0.5 pivot
- Gamma 0.50x to 2.00x as a `1/gamma` power curve
- Neutral values (1.00 on all three) bypass the color math entirely
- Shader file is always rewritten on apply, so reloads never lose it
- Settings persist in `~/.config/maple-saturation-hyprland/settings.json`
- Catppuccin Mocha dark theme

## Install

```bash
paru -S maple-saturation-hyprland-git
```

Add the `screen_shader` line above to your Hyprland config, then run `hyprctl reload` once.

## Usage

```bash
maple-saturation-hyprland
```

## Dependencies

- Hyprland with `hyprctl`
- `python-pyqt6`

## Limitations

- Fixed to output index 0 (the internal panel on a laptop). External displays are never touched, and there is no output selector in the GUI.
- Only works under Hyprland. Other compositors have no `screen_shader` hook.
- Saturation near 4.00 clips highly saturated primaries; values up to roughly 2.50 stay natural.
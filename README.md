# Maple Saturation (Hyprland)

Screen color saturation, contrast, and gamma control for Hyprland via GLSL shaders.

Companion project for KDE Plasma: [maple-saturation-plasma](https://github.com/MapleProjects/maple-saturation-plasma).

## Features
- Real-time saturation, contrast, and gamma adjustment via individual GUI sliders (PyQt6)
- Physically accurate Rec. 709 linear-space saturation preserving exact hues and boosting all color tones evenly
- Independent perceptual contrast (pivot 0.5) and display gamma correction (power curve 1/gamma)
- Zero-overhead bypass on neutral defaults (1.00) with guaranteed shader persistence (no missing shader file errors in Hyprland)
- Per-output protection (eDP-1 boosted, HDMI external displays unaffected)
- Hotplug synchronization with `hdmi-saturation-toggle`
- Settings persistence in `~/.config/maple-saturation-hyprland/settings.json`
- Dark Catppuccin Mocha theme

## Install (AUR)
```bash
paru -S maple-saturation-hyprland-git
```

## Usage
```bash
maple-saturation-hyprland
```

## Dependencies
- Hyprland
- python-pyqt6
- hyprctl
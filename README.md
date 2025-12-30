# Mouse & Monitor Configuration

Auto-switching mouse profiles, monitor sphere lighting, and RGB peripherals based on active application.

## Components

### Mouse Control (Logitech G502)
- **ratbag-profile-switcher**: Main daemon that switches profiles based on active window
- **hidpp-dpi**: Direct HID++ control for exact DPI (6400) and LED settings
- **ratbag-profiles.json**: Profile definitions (brave, kitty, code, overwatch, gimp)

### Monitor Control (LG 27GN950)
- **sphere-light**: RGB sphere lighting controller
- **monitor-ctl**: DDC/CI monitor controls (brightness, contrast, RGB, input switching)

### RGB Peripherals (OpenRGB)
- **OpenRGB integration**: Controls fans, RAM, and other RGB devices
- Supports all OpenRGB-compatible devices (motherboard RGB headers, RAM, etc.)

## Installation

```bash
# Install binaries
cp bin/* ~/.local/bin/
chmod +x ~/.local/bin/{ratbag-profile-switcher,sphere-light,monitor-ctl,hidpp-dpi}

# Install config
cp config/ratbag-profiles.json ~/.config/

# Install systemd service
cp systemd/ratbag-profile-switcher.service ~/.config/systemd/user/
systemctl --user enable --now ratbag-profile-switcher.service
```

## Features

- **Auto profile switching**: Detects active window (Brave, Kitty, Overwatch, etc.) and switches mouse buttons + lighting
- **Unified lighting control**: Mouse LED, Powerplay LED, monitor sphere lighting, and OpenRGB devices
- **Advanced lighting modes**: Supports static, breathing, cycle modes with brightness and speed control
- **Fast switching**: <2 seconds for 11 button reconfiguration using batched commits
- **Flicker prevention**: Caches lighting state to avoid redundant updates
- **Flexible config format**: Supports both simple color strings and full lighting objects (mode, brightness, speed)

## Profile Colors

- Default: Purple (all profiles inherit this unless overridden)

## Dependencies

- ratbagd / ratbagctl
- python3-hid
- hidapi
- ddcutil (for monitor control)
- openrgb (for RGB peripheral control)
- hyprctl (for window detection on Hyprland)

## Configuration Format

The config file `~/.config/ratbag-profiles.json` supports:

### Lighting Objects (New Format)
```json
{
  "led": {
    "mode": "breathing",
    "color": [128, 0, 255],
    "brightness": 255
  },
  "sphere_light": {
    "mode": "static",
    "color": "8000ff",
    "brightness": 100
  },
  "openrgb_devices": {
    "ASRock B650 PG Lightning": {
      "mode": "static",
      "color": "8000ff",
      "brightness": 100,
      "speed": 50
    }
  }
}
```

### Legacy Format (Still Supported)
```json
{
  "led_mode": "breathing",
  "led_color": [128, 0, 255],
  "sphere_light_color": "8000ff"
}
```

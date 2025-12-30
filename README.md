# Mouse & Monitor Configuration

Auto-switching mouse profiles and monitor sphere lighting based on active application.

## Components

### Mouse Control (Logitech G502)
- **ratbag-profile-switcher**: Main daemon that switches profiles based on active window
- **hidpp-dpi**: Direct HID++ control for exact DPI (6400) and LED settings
- **ratbag-profiles.json**: Profile definitions (brave, kitty, code, overwatch, gimp)

### Monitor Control (LG 27GN950)
- **sphere-light**: RGB sphere lighting controller
- **monitor-ctl**: DDC/CI monitor controls (brightness, contrast, RGB, input switching)

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

- **Auto profile switching**: Detects active window (Brave, Kitty, Overwatch, etc.) and switches mouse buttons + sphere lighting
- **Custom RGB**: Full RGB control for both mouse LED and monitor sphere lighting per profile
- **Fast switching**: <2 seconds for 11 button reconfiguration using batched commits
- **Flicker prevention**: Caches sphere lighting state to avoid redundant updates

## Profile Colors

- Default: Red
- Brave: Blue
- Kitty: Green
- Overwatch: Orange
- GIMP: Purple

## Dependencies

- ratbagd / ratbagctl
- python3-hid
- hidapi
- ddcutil (for monitor control)
- hyprctl (for window detection on Hyprland)

# Rofi Configuration by Hanashiko

A complete Rofi configuration featuring the Tokyo Night color scheme with custom scripts for application launching, power management, and password prompts.

## Overview

This Rofi configuration provides a modern, Tokyo Night-themed interface for:
- Application launcher
- Power menu with system controls
- Password/authentication prompts
- File browser support

## Features

- **Tokyo Night Color Scheme**: Beautiful dark theme with blue accents
- **Custom Scripts**: Ready-to-use scripts for common tasks
- **Icon Support**: Configurable icon display
- **Confirmation Dialogs**: Safe power actions with user confirmation
- **Multiple Modes**: Support for applications, commands, and file browsing

## Directory Structure

```
~/.config/rofi/
├── bin/
│   ├── askpass          # Password prompt script
│   ├── launcher         # Application launcher script
│   └── powermenu        # Power management script
└── config/
    ├── askpass.rasi     # Password prompt theme
    ├── colors.rasi      # Tokyo Night color definitions
    ├── confirm.rasi     # Confirmation dialog theme
    ├── font.rasi        # Font configuration
    ├── launcher.rasi    # Application launcher theme
    └── powermenu.rasi   # Power menu theme
```

## Scripts

### Launcher (`bin/launcher`)
Application launcher with the following features:
- Shows desktop applications (`drun` mode)
- Displays application names only
- Uses Terminator as default terminal
- Escape key to cancel
- Grid layout with icons (6 columns × 3 rows)

**Usage:**
```bash
~/.config/rofi/bin/launcher
```

### Power Menu (`bin/powermenu`)
Comprehensive power management with options for:
- **Shutdown**: Power off the system
- **Restart**: Reboot the system
- **Lock**: Lock the screen (requires `~/Bin/lock.sh`)
- **Sleep**: Suspend system with audio/music pause
- **Logout**: Exit i3 window manager

All power actions (except lock) require confirmation for safety.

**Usage:**
```bash
~/.config/rofi/bin/powermenu
```

### Ask Password (`bin/askpass`)
Simple password prompt dialog for authentication needs.

**Usage:**
```bash
~/.config/rofi/bin/askpass
```

## Color Scheme (Tokyo Night)

The configuration uses the Tokyo Night color palette:

| Color | Hex Code | Usage |
|-------|----------|-------|
| Background | `#1a1b26` | Main background |
| Background Alt | `#32344a` | Secondary background |
| Foreground | `#a9b1d6` | Main text color |
| Accent | `#7aa2f7` | Accent/selection color |
| Urgent | `#f7768e` | Urgent/warning color |

## Fonts

The configuration uses **RecMonoCasual Nerd Font**:
- Default: `RecMonoCasual Nerd Font Bold 18`
- Launcher elements: `Manrope Medium 12-14`
- Icons: `RecMonoCasual Nerd Font 10`

## Configuration Details

### Main Window Properties
- **Size**: 1000px width
- **Border**: 2px with 12px radius
- **Transparency**: Real transparency support
- **Position**: Center screen

### Launcher Configuration
- **Modes**: `drun`, `run`, `filebrowser`
- **Layout**: 6 columns, 3 rows
- **Icons**: Enabled (64px size)
- **Search**: Fuzzy matching across all fields

### Power Menu Features
- **Uptime Display**: Shows system uptime in prompt
- **Icon Options**: Two icon sets available (configurable)
- **Safety**: Confirmation required for destructive actions
- **Audio Integration**: Pauses music and mutes audio before suspend

## Dependencies

### Required
- **Rofi**: The application launcher
- **systemctl**: For power management
- **uptime**: For system uptime display

### Optional
- **Terminator**: Default terminal (configurable)
- **i3**: Window manager (for logout function)
- **mpc**: Music player control (for suspend)
- **amixer**: Audio control (for suspend)
- **lock script**: Custom lock script at `~/Bin/lock.sh` or `~/.local/bin/lock`

## Installation

1. **Clone repository:**
    ```bash
    git clone https://github.com/Hanashiko/dotfiles-rofi.git
    cd dotfiles-rofi
    ```

2. **Copy configuration files:**
   ```bash
   mkdir -p ~/.config/rofi/{bin,config}
   cp bin/* ~/.config/rofi/bin/
   cp config/* ~/.config/rofi/config/
   ```

3. **Make scripts executable:**
   ```bash
   chmod +x ~/.config/rofi/bin/*
   ```

4. **Install required fonts:**
   - RecMonoCasual Nerd Font
   - Manrope font family

## Usage Examples

### Bind to Keyboard Shortcuts

Add these to your window manager configuration:

```bash
# Application launcher
bindsym $mod+d exec ~/.config/rofi/bin/launcher

# Power menu
bindsym $mod+Shift+e exec ~/.config/rofi/bin/powermenu

# Quick password prompt
bindsym $mod+p exec ~/.config/rofi/bin/askpass
```

### Dmenu Replacement

Use Rofi scripts as dmenu replacement:
```bash
echo "option1\noption2\noption3" | rofi -dmenu -theme ~/.config/rofi/config/launcher.rasi
```

## Customization

### Changing Colors
Edit `config/colors.rasi` to modify the color scheme:
```css
* {
    BG:    #your-bg-color;
    ACC:   #your-accent-color;
    FG:    #your-text-color;
}
```

### Modifying Layout
Adjust columns and rows in the respective `.rasi` files:
```css
listview {
    columns: 6;  /* Number of columns */
    lines: 3;    /* Number of rows */
}
```

### Icon Configuration
Toggle icons in launcher by modifying:
```css
configuration {
    show-icons: true;  /* or false */
}
```

## Troubleshooting

### Icons Not Displaying
1. Ensure Nerd Font is installed and properly configured
2. Check if icon theme is available
3. Try the alternative icon section in powermenu script

### Permission Issues
Ensure scripts are executable:
```bash
ls -la ~/.config/rofi/bin/
chmod +x ~/.config/rofi/bin/*
```

### Power Actions Not Working
Verify systemctl permissions and dependencies:
```bash
# Test systemctl commands
systemctl --dry-run poweroff
systemctl --dry-run reboot
```

## Credits

- **Color Scheme**: Tokyo Night
- **Fonts**: RecMonoCasual Nerd Font, Manrope
- **Icons**: Nerd Font icons

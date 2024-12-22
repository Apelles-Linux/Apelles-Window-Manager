# Apelles Window Manager

Apelles is a dynamic tiling window manager based on the suckless philosophy. It's a fork of dwm with additional features and customizations, focusing on simplicity, efficiency, and keyboard-driven workflow.

## Table of Contents
- [Features](#features)
- [Installation](#installation)
- [Configuration](#configuration)
- [Layouts](#layouts)
- [Keybindings](#keybindings)
- [Mouse Controls](#mouse-controls)
- [Autostart](#autostart)
- [Scratchpads](#scratchpads)
- [Window Rules](#window-rules)
- [Status Bar](#status-bar)
- [Patches and Extensions](#patches-and-extensions)
- [Customization](#customization)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)

## Features

Core features include:
- Dynamic window tiling
- Multiple layouts
- Customizable gaps between windows
- Floating window support
- Window ***Swallowing*** capability
- ***Scratchpad*** terminals
- Multi-monitor support
- Status bar with customizable colors
- *.Xresources* integration
- Custom window factor adjustments
- Automatic window rules
- Window cycling

## Installation

### Dependencies
- Xlib headers
- libXinerama
- libXft
- dmenu (program launcher)
- st (default terminal)
- JetBrainsMono Nerd Font
- slstatus (status bar)
- ranger (optional, for file manager scratchpad)
- make
- gcc

### Building from Source
```bash
git clone https://github.com/ayusjayaswal/Apelles-Window-Manager.git
cd Apelles-Window-Manager
sudo make clean install
```

### Post-Installation
 
Move dwm.desktop to the _/usr/share/xsessions/_ folder

## Configuration

### config.h
Main configuration is done through `config.def.h`. Key aspects that can be configured:
- Keybindings
- Layouts
- Fonts
- Colors
- Border width
- Gap sizes
- Autostart programs
- Window rules

### Xresources
Create `~/.Xresources` with these configurations:

```xresources
! DWM Base Colors
dwm.normfgcolor: #ebdbb2
dwm.normbgcolor: #282828
dwm.normbordercolor: #282828
dwm.selfgcolor: #282828
dwm.selbgcolor: #83a598
dwm.selbordercolor: #83a598

! Layout Settings
dwm.borderpx: 2
dwm.gappx: 8
dwm.snap: 32
dwm.showbar: 1
dwm.topbar: 1

! Window Management
dwm.nmaster: 1
dwm.resizehints: 1
dwm.mfact: 0.55

! Terminal Colors (Gruvbox)
*.foreground: #ebdbb2
*.background: #282828
*.cursorColor: #ebdbb2

! Black + DarkGrey
*.color0: #282828
*.color8: #928374
! DarkRed + Red
*.color1: #cc241d
*.color9: #fb4934
! DarkGreen + Green
*.color2: #98971a
*.color10: #b8bb26
! DarkYellow + Yellow
*.color3: #d79921
*.color11: #fabd2f
! DarkBlue + Blue
*.color4: #458588
*.color12: #83a598
! DarkMagenta + Magenta
*.color5: #b16286
*.color13: #d3869b
! DarkCyan + Cyan
*.color6: #689d6a
*.color14: #8ec07c
! LightGrey + White
*.color7: #a89984
*.color15: #ebdbb2
```

Apply changes with:
```bash
xrdb -merge ~/.Xresources
```

## Layouts

Available layouts:
1. `STK` - Traditional tiling (master-stack)
   - One master window on the left, stack on the right
   - Adjustable master width
   
2. `[M]` - Monocle
   - All windows fullscreen
   - Cycle through with keybindings
   
3. `SPR` - Spiral
   - Windows arranged in fibonacci spiral
   - Good for many windows
   
4. `DCK` - Deck
   - Master window with stacked windows
   - Like a card deck
   
5. `BST` - Bottom stack
   - Master window on top
   - Stack arranged horizontally below
   
6. `GRD` - Grid
   - Equal-sized grid arrangement
   - Automatically adjusts to window count
   
7. `NGD` - N-row grid
   - Grid with customizable rows
   - Forced vertical splits available
   
8. `CST` - Centered master
   - Master window in center
   - Other windows on sides
   
9. `FLT` - Floating
   - Free window placement
   - Traditional stacking window manager

## Keybindings

MODKEY is set to the Windows key (Mod4)

### Core Controls
- `MODKEY + Enter` - Open terminal
- `MODKEY + Shift + Enter` - Open dmenu
- `MODKEY + b` - Toggle status bar
- `MODKEY + x` - Kill focused window
- `MODKEY + Shift + q` - Quit Apelles
- `MODKEY + Ctrl + Shift + q` - Restart Apelles

### Window Management
- `MODKEY + w` - Focus next window
- `MODKEY + s` - Focus previous window
- `MODKEY + Shift + w` - Move window up in stack
- `MODKEY + Shift + s` - Move window down in stack
- `MODKEY + q` - Zoom/Switch to master
- `MODKEY + f` - Toggle fullscreen
- `MODKEY + Space` - Toggle between layouts
- `MODKEY + Shift + Space` - Toggle floating
- `MODKEY + Tab` - Cycle through layouts forward
- `MODKEY + Shift + Tab` - Cycle through layouts backward

### Master Area
- `MODKEY + a` - Increase number of master windows
- `MODKEY + d` - Decrease number of master windows
- `MODKEY + h` - Decrease master area size
- `MODKEY + l` - Increase master area size

### Window Resizing
- `MODKEY + Shift + h` - Increase client size horizontally
- `MODKEY + Shift + l` - Decrease client size horizontally

### Tags (Workspaces)
- `MODKEY + 1-9` - Switch to tag 1-9
- `MODKEY + Shift + 1-9` - Move window to tag 1-9
- `MODKEY + Ctrl + 1-9` - Toggle tag view
- `MODKEY + 0` - View all tags
- `MODKEY + Shift + 0` - Tag window with all tags

### Gaps
- `MODKEY + g`               - Toggle gaps
- `MODKEY + Shift + g`       - Reset gaps to default
- `MODKEY + Alt + u`         - Increase all gaps
- `MODKEY + Alt + Shift + u` - Decrease all gaps
- `MODKEY + Alt + i`         - Increase inner gaps
- `MODKEY + Alt + Shift + i` - Decrease inner gaps
- `MODKEY + Alt + o`         - Increase outer gaps
- `MODKEY + Alt + Shift + o` - Decrease outer gaps

### Multi-monitor
- `MODKEY + comma/period` - Focus previous/next monitor
- `MODKEY + Shift + comma/period` - Move window to previous/next monitor

### Scratchpads
- `MODKEY + c` - Toggle terminal scratchpad
- `MODKEY + v` - Toggle ranger file manager scratchpad

## Mouse Controls

- `MODKEY + Left Click` - Move window
- `MODKEY + Right Click` - Resize window
- `MODKEY + Middle Click` - Toggle floating
- Click on tag - Switch to tag
- Right click on tag - Toggle tag view
- `MODKEY + Click` on tag - Move window to tag
- Click on layout symbol - Cycle layouts

## Autostart

Programs can be automatically started by adding them to the `autostart` array in `config.h`:

```c
static const char *const autostart[] = {
    "slstatus", NULL,
    "nitrogen", "--restore", NULL,  // Wallpaper
    "picom", NULL,                  // Compositor
    "nm-applet", NULL,              // Network manager
    NULL /* terminate */
};
```

## Window Rules

Window rules are defined in `config.def.h`. Example configuration:

```c
static const Rule rules[] = {
    /* class      instance    title       tags mask     isfloating   isterminal  noswallow  monitor */
    { "Gimp",     NULL,       NULL,       0,            1,           0,          0,        -1 },
    { "Firefox",  NULL,       NULL,       1 << 8,       0,           0,         -1,        -1 },
    { "st",       NULL,       NULL,       0,            0,           1,          0,        -1 },
    { NULL,       "spterm",   NULL,       SPTAG(0),     1,           1,          0,        -1 },
};
```

## Status Bar

The status bar uses slstatus. To customize:
1. Clone and build slstatus
2. Configure status bar items in slstatus's config.h
3. Restart Apelles

## Patches and Extensions

Common patches that can be applied:
- systray (system tray support)
- pertag (per-tag layout settings)
- fullgaps (advanced gap customization)
- attachaside (new windows added to stack)
- alpha (transparency support)
- vanity gaps (advanced gap settings)
- swallow (terminal window swallowing)
- cool-autostart (enhanced autostart)

## Customization

### Adding New Layouts
1. Create new layout function in `layouts.c`
2. Add to `layouts[]` array in `config.h`
3. Recompile

### Custom Colors
1. Edit colors in `.Xresources`
2. Run `xrdb -merge ~/.Xresources`
3. Restart Apelles

### Custom Status Bar
1. Modify slstatus configuration
2. Recompile slstatus
3. Restart status bar

## Troubleshooting

Common issues and solutions:

1. Black screen after starting:
   - Check .xinitrc
   - Verify X server running
   - Check logs in ~/.local/share/xorg/

2. No status bar:
   - Verify slstatus installed
   - Check autostart configuration
   - Try running slstatus manually

3. Font issues:
   - Install JetBrainsMono Nerd Font
   - Check font configuration in config.h
   - Verify Xresources loading

## Contributing

1. Fork the repository
2. Create feature branch
3. Commit changes
4. Push to branch
5. Create Pull Request

Follow suckless coding style:
- Clear, simple code
- Minimal dependencies
- Avoid bloat
- Keep patches separate

## License

See LICENSE file for details. Based on dwm, which is licensed under the MIT/X Consortium License.

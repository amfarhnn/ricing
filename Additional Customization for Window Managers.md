### Additional Customizations for Window Managers (WM)

Customizing a Window Manager (WM) involves enhancing its appearance, functionality, and efficiency to suit your workflow. Here's a detailed guide focused on additional customizations for popular WMs like i3, bspwm, and Hyprland.

#### i3 Window Manager

**Configuration File**:
- The main configuration file for i3 is located at `~/.config/i3/config`.
- Example basic configuration:
  ```bash
  # Set mod key (Mod4 is the Super key)
  set $mod Mod4

  # Launch terminal
  bindsym $mod+Return exec alacritty

  # Close focused window
  bindsym $mod+Shift+q kill

  # Restart i3 in place (preserves your layout/session, can be used to upgrade i3)
  bindsym $mod+Shift+r restart

  # Exit i3
  bindsym $mod+Shift+e exec "i3-nagbar -t warning -m 'Do you really want to exit i3?' -B 'Yes' 'i3-msg exit'"
  ```

**Status Bar**:
- **i3status**: A simple status bar for i3.
  - Installation: `sudo pacman -S i3status`
  - Configuration: Edit the configuration file at `~/.config/i3status/config`.
  - Example:
    ```bash
    general {
        colors = true
        interval = 5
    }

    order += "disk /"
    order += "cpu_usage"
    order += "load"

    disk "/" {
        format = "Disk: %avail"
    }

    cpu_usage {
        format = "CPU: %usage"
    }

    load {
        format = "Load: %1min"
    }
    ```

- **Polybar**: A more customizable and feature-rich status bar.
  - Installation: `sudo pacman -S polybar`
  - Configuration: Create and edit the configuration file at `~/.config/polybar/config`.
  - Example configuration:
    ```bash
    [bar/example]
    width = 100%
    height = 30
    background = #222
    foreground = #dfdfdf

    modules-left = i3
    modules-center = 
    modules-right = cpu memory date

    [module/i3]
    type = internal/i3
    ```
  - Launch Polybar by adding it to your startup script:
    ```bash
    polybar example &
    ```

#### bspwm Window Manager

**Configuration Files**:
- bspwm uses a shell script for its configuration located at `~/.config/bspwm/bspwmrc`.
  - Example:
    ```bash
    #!/bin/sh
    bspc monitor -d I II III IV V VI VII VIII IX X
    bspc config border_width 2
    bspc config window_gap 8
    bspc config split_ratio 0.52
    bspc config borderless_monocle true
    bspc config gapless_monocle true
    ```

- **sxhkd**: Simple X Hotkey Daemon is used for keybindings, configured at `~/.config/sxhkd/sxhkdrc`.
  - Example:
    ```bash
    # Launch terminal
    super + Return
        alacritty

    # Close focused window
    super + Shift + q
        bspc node -c

    # Swap the current window with the biggest window
    super + g
        bspc node -s biggest
    ```

**Status Bar**:
- **Polybar**: Commonly used with bspwm as well.
  - Configuration: Same as i3, edit `~/.config/polybar/config`.

#### Hyprland Window Manager

**Installation**:
- Refer to the [Hyprland GitHub repository](https://github.com/hyprwm/Hyprland) for installation instructions.

**Configuration Files**:
- Configuration is typically done in `~/.config/hypr/hyprland.conf`.
  - Example:
    ```bash
    [general]
    gaps_in = 5
    gaps_out = 20
    border_size = 2
    rounding = 5
    shadow = true

    [monitor]
    monitor = eDP-1, 1920x1080@60, 1, 0, 0, 1
    ```

- **Keybindings**:
  - Add keybindings directly in the configuration file or use a separate keybinding manager if preferred.
  - Example:
    ```bash
    bind = super + Return, exec, alacritty
    bind = super + Shift + q, exec, pkill alacritty
    ```

**Status Bar**:
- **Waybar**: A customizable status bar for Wayland.
  - Installation: `sudo pacman -S waybar`
  - Configuration: Create and edit `~/.config/waybar/config` and `~/.config/waybar/style.css`.
  - Example configuration:
    ```bash
    {
        "layer": "top",
        "position": "top",
        "modules-left": ["clock"],
        "modules-center": [],
        "modules-right": ["cpu", "memory", "temperature", "battery", "network"]
    }
    ```
  - Example style:
    ```css
    * {
        font-family: "Roboto";
        font-size: 12px;
    }

    #clock {
        color: #ffffff;
    }

    #cpu, #memory, #temperature, #battery, #network {
        color: #dfdfdf;
    }
    ```

#### Additional Tools and Utilities

**Compositors**:
- **Picom**: Adds transparency, shadows, and other visual effects.
  - Installation: `sudo pacman -S picom`
  - Configuration: Create a configuration file at `~/.config/picom.conf`.
  - Example:
    ```bash
    opacity-rule = [
      "90:class_g = 'Alacritty'"
    ];
    ```

**Notification Daemons**:
- **Dunst**: A lightweight and customizable notification daemon.
  - Installation: `sudo pacman -S dunst`
  - Configuration: Create a configuration file at `~/.config/dunst/dunstrc`.
  - Example:
    ```bash
    [global]
    geometry = "300x50-20+20"
    frame_color = "#aaaaaa"
    ```

**File Managers**:
- **Ranger**: CLI-based file manager.
  - Installation: `sudo pacman -S ranger`
- **Thunar**: GUI-based file manager.
  - Installation: `sudo pacman -S thunar`

**Terminal Emulators**:
- **Alacritty**:
  - Installation: `sudo pacman -S alacritty`
- **Kitty**:
  - Installation: `sudo pacman -S kitty`

By focusing on these customizations, you can tailor your Window Manager to fit your specific needs and preferences, creating a highly efficient and personalized environment.
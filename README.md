# Dotfiles

My current set of dotfiles. Attempts to establish the same desktop environment across the Sway, Hyprland, and Niri compositors. Dotfiles are not always equally maintained, so one set may be outdated.

## Keybinds

Across all configurations, the following keybinds are available. (<kbd>Mod</kbd> = Windows key)

| Action                 | Keybind                                      |
| ---------------------- | -------------------------------------------- |
| Open terminal          | <kbd>Mod</kbd>+<kbd>Enter</kbd>              |
| Program launcher       | <kbd>Mod</kbd>+<kbd>D</kbd>                  |
| Close window           | <kbd>Mod</kbd>+<kbd>Shift</kbd>+<kbd>Q</kbd> |
| Move window            | <kbd>Mod</kbd>+<kbd>Left Mouse</kbd>         |
| Resize window          | <kbd>Mod</kbd>+<kbd>Right Mouse</kbd>        |
| Toggle tabbed layout   | <kbd>Mod</kbd>+<kbd>W</kbd>                  |
| Toggle fullscreen view | <kbd>Mod</kbd>+<kbd>F</kbd>                  |
| Take a screenshot      | <kbd>PrntScr</kbd>                           |
| Exit compositor        | <kbd>Mod</kbd>+<kbd>Shift</kbd>+<kbd>E</kbd> |

## Setup cheat sheet

Written for Arch Linux.

### Global

```sh
# Packages
sudo pacman -S uwsm hyprpicker xdg-desktop-portal-gtk mako waybar wl-copy grim slurp wmenu j4-dmenu-desktop foot

# User services
systemctl --user enable --now waybar.service

# Add this into `.bash_profile` (EXCEPT IF YOU'RE ON NIRI; READ BELOW)
export GTK_THEME=Adwaita:dark
if uwsm check may-start && uwsm select; then
  exec systemd-cat -t uwsm_start uwsm start default
fi
```

### Hyprland

```sh
# Packages
sudo pacman -S hyprland hyprpaper hypridle hyprlock xdg-desktop-portal-hyprland hyprpolkitagent dolphin swayimg

# User services
systemctl --user enable --now hyprpaper.service
systemctl --user enable --now hypridle.service
```

### Sway

```sh
# Packages
sudo pacman -S sway swaylock swayidle swaybg dolphin swayimg
```

### Niri

[Niri](https://github.com/YaLTeR/niri) works best with GDM, therefore `uwsm` isn't necessary. Instead of KDE apps to provide system basics, we use GNOME's (for better or for worse).

```sh
# Packages
sudo pacman -S niri gdm xdg-desktop-portal-gnome gnome-keyring swaybg swayidle swaylock nautilus loupe

# Enable display manager
systemctl enable gdm

# Enable dark mode
dconf write /org/gnome/desktop/interface/color-scheme '"prefer-dark"'
```

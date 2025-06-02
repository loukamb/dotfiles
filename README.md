# Dotfiles

My current set of dotfiles. Attempts to establish the same desktop environment across the Sway, Hyprland, labwc, and Niri compositors. Dotfiles are not always equally maintained, so one set may be outdated.

## Keybinds

Across all configurations, the following keybinds are available. (<kbd>Mod</kbd> = Windows key)

| Action                 | Keybind                                      |
| ---------------------- | -------------------------------------------- |
| Open terminal          | <kbd>Mod</kbd>+<kbd>Enter</kbd>              |
| Program launcher       | <kbd>Mod</kbd>+<kbd>D</kbd>                  |
| Close window\*         | <kbd>Mod</kbd>+<kbd>Shift</kbd>+<kbd>Q</kbd> |
| Move window            | <kbd>Mod</kbd>+<kbd>Left Mouse</kbd>         |
| Resize window\*        | <kbd>Mod</kbd>+<kbd>Right Mouse</kbd>        |
| Toggle tabbed layout\* | <kbd>Mod</kbd>+<kbd>W</kbd>                  |
| Toggle fullscreen view | <kbd>Mod</kbd>+<kbd>F</kbd>                  |
| Take a screenshot      | <kbd>PrntScr</kbd>                           |
| Exit compositor\*      | <kbd>Mod</kbd>+<kbd>Shift</kbd>+<kbd>E</kbd> |

<font style="font-size: 0.7em;">\*Not available on labwc, since it is a stacking compositor, not a tiling one.</font>

## Setup cheat sheet

Written for Arch Linux.

### Global

#### Dependencies

```sh
# Packages
sudo pacman -S uwsm hyprpicker xdg-desktop-portal-gtk mako waybar wl-clipboard grim slurp wmenu j4-dmenu-desktop foot archlinux-xdg-menu

# User services
systemctl --user enable --now waybar.service

# Setup MIME types.
sudo ln -s /etc/xdg/menus/arch-applications.menu /etc/xdg/menus/applications.menu

# Add this into `.bash_profile` (EXCEPT IF YOU'RE ON NIRI; READ BELOW)
export GTK_THEME=Adwaita:dark
if uwsm check may-start && uwsm select; then
  exec systemd-cat -t uwsm_start uwsm start default
fi
```

#### Waybar

Make sure to delete the existing `config.jsonc` symlink and rename one of the `config.jsonc.*` files in `waybar` to `config.jsonc`. The existing symlink points to `config.jsonc.sway`.

**NOTE:** Keyboard layout isn't supported on `labwc` due to the compositor's strict adherance to wlroots protocols.

#### vim

Copy `.vimrc` into your home directory (`~/.vimrc`).

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
sudo pacman -S sway swaylock swayidle swayimg swaybg dolphin
```

### labwc

#### Notes

- Certain keybinds are not available due to labwc being a _stacking_ compositor instead of a _tiling_ one.
- labwc prefers `alacritty` over `foot` as the terminal emulator.
- labwc provides no mechanism for output configuration, so `wlr-randr` is used to adjust monitors. Edit `/labwc/autostart` to configure.

```sh
# Packages
sudo pacman -S labwc swaylock swayidle swayimg swaybg dolphin alacritty wlr-randr
```

### Niri

#### Notes

- [Niri](https://github.com/YaLTeR/niri) works best with GDM, therefore `uwsm` isn't necessary. Instead of KDE apps to provide system basics, we use GNOME's (for better or for worse).

```sh
# Packages
sudo pacman -S niri gdm xdg-desktop-portal-gnome gnome-keyring swaybg swayidle swaylock nautilus sushi loupe gnome-text-editor

# Enable display manager
systemctl enable gdm

# Enable dark mode
dconf write /org/gnome/desktop/interface/color-scheme '"prefer-dark"'
```

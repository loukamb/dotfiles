# Dotfiles

My current set of dotfiles. Previously used Sway, but lack of functionality made me switch to Hyprland.

## Packages

```sh
uwsm hyprland hyprpaper hypridle hyprlock xdg-desktop-portal-gtk xdg-desktop-portal-hyprland hyprpolkitagent mako waybar wl-copy grim slurp

# Enable user units (possible thanks to uwsm)
systemctl --user enable --now waybar.service
systemctl --user enable --now hyprpaper.service
systemctl --user enable --now hypridle.service

# Add this into `.bash_profile`
export GTK_THEME=Adwaita:dark
if uwsm check may-start && uwsm select; then
  exec systemd-cat -t uwsm_start uwsm start default
fi
```

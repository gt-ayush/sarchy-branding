# sarchy-branding

Branding package for **Sarchy** — an Artix Linux–based OS (Artix is Arch-based, using OpenRC/runit/s6 instead of systemd).  
Part of the [Sarchy-iso](https://github.com/gt-ayush/Sarchy-iso) project.

## What's included

| Asset | Location |
|-------|----------|
| Wallpaper (PNG) | `usr/share/backgrounds/sarchy/sarchy-wallpaper.png` |
| App icon (PNG, multiple sizes) | `usr/share/icons/hicolor/{16,32,64,128,256,512,scalable}/apps/sarchy.png` |
| Plymouth boot theme | `usr/share/plymouth/themes/sarchy/` |
| GRUB theme | `usr/share/grub/themes/sarchy/` |
| SDDM theme | `usr/share/sddm/themes/sarchy/` |

## Build & install

This is a standard Arch `makepkg` package. All source files are shipped in the repo, so there are no remote downloads.

```bash
# Build the package
makepkg -s

# Install the resulting package
sudo pacman -U sarchy-branding-1.0.0-1-any.pkg.tar.zst
```

## Apply the themes after install

The `.install` hook attempts to set the Plymouth theme and regenerate GRUB config, but you should confirm:

```bash
# Plymouth boot splash (works on Artix too; optional if you use a plain framebuffer console)
sudo plymouth-set-default-theme -R sarchy 2>/dev/null || true

# GRUB theme — edit /etc/default/grub, then:
GRUB_THEME="/usr/share/grub/themes/sarchy/theme.txt"
sudo grub-mkconfig -o /boot/grub/grub.cfg

# SDDM — set the background in /etc/sddm.conf:
# [Theme]
# Current=sarchy
```

### Artix notes

Artix uses OpenRC/runit/s6 rather than systemd, so Plymouth isn't part of the default boot path the way it is on Arch. If you don't run Plymouth, the wallpaper and icon still apply to your desktop/SDM, and the GRUB theme works regardless of init system.


## License

GPL-3.0-or-later — see `LICENSE`.

# ROGueENEMY PKGBUILD
This is the Arch Linux package for the [ROGueENEMY](https://github.com/NeroReflex/ROGueENEMY) project.

## Usage
To use this package compile it, install it and use the provided systemd service file:

```sh
makepkg -sfi
sudo systemctl daemon-reload
sudo systemctl enable rogue-enemy
```

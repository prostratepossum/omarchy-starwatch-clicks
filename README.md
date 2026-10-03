# Starwatch Clicks

A tiny firefly burst wherever you click, for [Omarchy](https://omarchy.org).

![preview](preview.gif)

- **left click**: fireflies scatter out of a soft ring
- **right click**: lavender sparkles (✦) twinkle outwards
- **middle click**: a glacier-blue ripple

The overlay is click-through and only exists while a burst is playing. Nothing plays over fullscreen windows (games, video). It looks best with the [Alpine Marmot theme](https://github.com/prostratepossum/omarchy-alpine-marmot-theme).

## Install

```bash
sudo pacman -S python-evdev
sudo usermod -aG input $USER   # then log out and back in
omarchy plugin add https://github.com/prostratepossum/omarchy-starwatch-clicks --enable
```

## How it works

Wayland doesn't tell other programs about your clicks, so a small helper (`clickwatch.py`) reads mouse button presses straight from `/dev/input` with python-evdev. It only opens mouse-type devices (never keyboards) and only reads button-down events, not movement. The click position comes from Hyprland's `cursorpos`. Mice you plug in later are picked up within a few seconds.

Being in the `input` group lets any program you run read input devices, keyboards included. If that trade-off isn't for you, don't install this plugin.

## Try it

```bash
omarchy-shell -q clicks test     # a burst in the middle of the screen
omarchy-shell -q clicks toggle   # turn it on/off
```

## Remove

```bash
omarchy plugin remove io.github.prostratepossum.starwatch-clicks
```

## Troubleshooting

No bursts? Check that `python3 -c 'import evdev'` works and that `id -nG` lists `input`. Running `/usr/bin/python3 clickwatch.py` from the plugin folder prints a line per click, or a message saying what's missing.

## License

MIT. See [LICENSE](LICENSE).

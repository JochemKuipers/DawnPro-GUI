# DawnPro-GUI
DawnPro-GUI is a tool used to control the Moondrop Dawn Pro AMP/DAC.

![screenshot](preview.png)

## Features

- Change the LED status (on, temp-off, off)
- Set the gain (low, high)
- Configure the filters:
    - Fast-roll-off-low-latency
    - Fast-roll-off-phase-compensated
    - Slow-roll-off-low-latency
    - Slow-roll-off-phase-compensated
    - Non-oversampling
- Adjust the volume
- Fully configurable through JSON configuration file

## Requirements

- Python 3
- `pyusb`
- `PyGObject` / GTK 3

## Installation

### From APT (Debian / Ubuntu)

```sh
curl -fsSL https://jochemkuipers.github.io/apt-repo/jochem.sources \
  | sudo tee /etc/apt/sources.list.d/jochem.sources
sudo apt update
sudo apt install dawnpro-gui
```

### Local Debian package

```sh
sudo apt-get install -y debhelper
dpkg-buildpackage -us -uc -b
sudo apt install ../dawnpro-gui_*.deb
```

### Manual

```sh
pip install -r requirements.txt
# PyGObject also needs system GTK: https://pygobject.gnome.org/
python3 main.py
```

For manual installs without the package, add a udev rule:

```sh
sudo cp udev/99-dawn-pro.rules /etc/udev/rules.d/
sudo udevadm control --reload-rules
sudo udevadm trigger
```

## Configuration

The application uses `~/.config/dawnpro/config.json`. If missing, built-in defaults apply.

```sh
mkdir -p ~/.config/dawnpro
cp config.json ~/.config/dawnpro/config.json
```

Sections: `device_constants`, `device_identifiers`, `default_settings`, `ui_metrics`, `logging`.

## Usage

Plug in the DAC/AMP, then run `dawnpro-gui` (or `python3 main.py`).

## Testing

```sh
pip install pytest
pytest
```

## Acknowledgments

Inspired by [mdrop](https://github.com/frahz/mdrop/) by frahz.

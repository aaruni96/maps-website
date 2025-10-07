---
title: "Installation"
description: "Installing the MaRDI Packaging System"
summary: ""
date: 2023-09-07T16:04:48+02:00
lastmod: 2023-09-07T16:04:48+02:00
draft: false
weight: 810
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

MaPS requires python 3.9 or above. Please make sure your OS, and python
environment accommodate this need. Almost all Linux distros still supported by
their vendors meet this requirement.

## Using a Package Manager

### Debian based systems

> Note, this requires a distribution which bundles the `python-tuspy` package,
> for example, Debian 12 and newer, or Ubuntu 24.04 and newer. Check
> [Repology](https://repology.org/project/python%3Atuspy/versions) for more
> details.

1. Download the maps installer in the `.deb` format from
   [MaPS Releases](https://github.com/mardI4NFDI/maps/releases/latest) .
2. Install this file using the terminal

   ```bash
   sudo apt install ./maps*.deb
   ```


### Arch based systems

MaPS is published on the Arch User Repository (aur). You can download and
install MaPS from the AUR.

#### Using an AUR helper

Install `maps` using your aur helper. For example, if you use `yay`, the command
is

```bash
yay -S maps
```

#### Manually

1. Install tuspy from the aur.

   ```bash
   git clone https://aur.archlinux.org/python-tuspy.git && cd python-tuspy
   makepkg -si
   ```

2. Install maps from the aur

   ```bash
   git clone https://aur.archlinux.org/maps.git && cd maps
   makepkg -si
   ```

### Fedora based systems

#### Make sure COPR is installed

```bash
sudo dnf install dnf-plugins-core
```

#### Enable the python3-tuspy and maps copr repositores

```bash
sudo dnf copr enable aaruni96/python3-tuspy
sudo dnf copr enable aaruni96/maps
```

#### Install MaPS using DNF

```bash
sudo dnf install maps
```

## From Source

### Dependencies

First install the dependencies.

#### APT based systems (Debian/Ubuntu/Mint/etc)

```bash
sudo apt install git libcairo2-dev gcc python3-dev libgirepository1.0-dev\
libostree-dev fuse-overlayfs python3-venv libcap-dev autoconf meson ostree
```

#### DNF based systems (Fedora/RHEL/CentOS/etc)

```bash
sudo dnf install git cairo-devel gcc python3-devel gobject-introspection-devel\
ostree-devel fuse-overlayfs libcap-devel autoconf cairo-gobject-devel meson\
ostree
```

#### pacman based systems (Arch Linux/Endeavour OS/Manjaro/etc)

```bash
sudo pacman -Sy base-devel cairo git gobject-introspection-runtime python3\
ostree fuse-overlayfs meson
```

### MaPS

Clone maps to somewhere convenient.

```bash
git clone https://github.com/MaRDI4NFDI/maps.git && cd maps
```

Setup a python venv, and install the python dependencies.

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Check that MaPS works

```bash
./src/maps --list
```

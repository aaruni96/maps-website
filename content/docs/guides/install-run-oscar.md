---
title: "Deploy and Run OSCAR"
description: ""
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

## MaPS Installation

### Required Software

First install the pre requisite software.

#### APT based systems (Debian/Ubuntu/Mint/etc)

```bash
sudo apt install git libcairo2-dev gcc python3-dev libgirepository1.0-dev libostree-dev python3-venv libcap-dev autoconf meson ostree
```

#### DNF based systems (Fedora/RHEL/CentOS/etc)

```bash
sudo dnf install git cairo-devel gcc python3-devel gobject-introspection-devel ostree-devel libcap-devel autoconf cairo-gobject-devel meson ostree
```

#### pacman based systems (Arch Linux/Endeavour OS/Manjaro/etc)

```bash
sudo pacman -Sy base-devel cairo git gobject-introspection-runtime python3 ostree meson
```

## MaPS

Clone maps to somewhere convenient.

```bash
$ git clone https://github.com/aaruni96/maps.git && cd maps
```

Setup a python venv, and install the python dependencies.

```bash
$ python3 -m venv .venv
$ source .venv/bin/activate
$ pip install -r requirements.txt
```

Check that MaPS works

```bash
$ python src/maps --list
```

## Deploy OSCAR

Once MaPS is running deploy and run OSCAR.

```bash
$ python src/maps -d org.oscar_system.oscar/x86_64/latest
$ python src/maps -r org.oscar_system.oscar/x86_64/latest
```

This will launch a shell inside the OSCAR runtime. Then launch julia inside the runtime.

```bash
root@runtime:~# julia
```

![oscar](https://github.com/aaruni96/maps/assets/7453256/b36e544e-a009-453c-8272-1eec7401caeb)

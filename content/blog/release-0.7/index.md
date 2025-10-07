---
title: "v0.7 Released!"
description: "test"
summary: "New version"
date: 2023-08-25T16:27:22+02:00
lastmod: 2023-08-25T16:27:22+02:00
draft: false
weight: 50
categories: []
tags: []
contributors: []
pinned: false
homepage: false
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

v0.7 has been released!

## Changelog

### Added

- **Bugfix**: Added `--gui` option to package mode.

### Changed

- Allow initialize into existing empty directory.
- Update list mode to include date when runtime was published
- `python3-tuspy` is now an optional dependency. Upload is disabled if it is not
  installed. This makes the `.deb` packages compatible with older releases of
  Debian and other downstream distros.
- Bugfix: Gracefully handle a repository not providing date information instead
  of crashing
- Bugfix: Handle the case when `XDG_SESSION_TYPE` is not set

### NOTE

> - The Arch Linux package can be installed from the AUR at
> [https://aur.archlinux.org/packages/maps](https://aur.archlinux.org/packages/maps)
> - The Fedora Linux package can be installed from COPR at
> [https://copr.fedorainfracloud.org/coprs/aaruni96/maps/](https://copr.fedorainfracloud.org/coprs/aaruni96/maps/)
> - `python3-tuspy` is only available in Debian 12+ and Ubuntu 24.04+. Upload
> functionality will be disabled on older Debian and Ubuntu systems, until
> python-tuspy is manually installed.

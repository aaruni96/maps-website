---
title: "Package Mode"
description: "Reference pages are ideal for outlining how things work in terse
              and clear terms."
summary: ""
date: 2023-09-07T16:13:18+02:00
lastmod: 2023-09-07T16:13:18+02:00
draft: false
weight: 920
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

This is the mode to use for authors trying to package a new runtime. In this
mode, runtimes can be created, commited, and uploaded.

As of version 0.7, the following options are available :

```text
  -c, --commit TREE BRANCH
                        Commit TREE to BRANCH in REPO
  -i, --initialize DIR  initialize DIR with a good base tree
  -s, --sandbox LOCATION
                        Start a sandbox at LOCATION
  -v, --verbose         enable verbose output
  --repo REPO           Repository to use
  -u, --upload RUNTIME  Upload RUNTIME for publishing.
  --no-gui              Disable GUI
  --gui                 Force enable GUI
```

## `--verbose`

Adding `-v` or `--verbose` to any command will run MaPS in verbose mode. This
prints a lot of extra information which might be helpful to investigate in case
things go wrong. Please include output in verbose mode whenever submitting a bug
report.

## `--initialize`

```bash
maps package -i <path-to-sandbox>
```

```bash
maps package --initialize <path-to-sandbox>
```

This option initializes the `<path-to-sandbox>` directory with the Debian
minimal image, as a way to quickly bootstrap the creation of a runtime. The
provided path must not exist, or must be an empty directory.

## `--sandbox`

```bash
maps package -s <path-to-sandbox>
```

```bash
maps package --sandbox <path-to-sandbox>
```

This option launches an interactive sandbox at the provided path. This should
ideally be the same path as given to the `--initialize` option, as, at least
bash (and its dependencies) are expected to be found. This is a mutable sandbox,
which will later be saved into a runtime. Use this interactive environment to
handcraft your (to be) runtime.

### A note on fakeroot

You cannot execute `chown`, `chgrp`, `chmod` etc while inside the runtime. This
is standard behaviour of Linux user namespaces. This is not a choice made by
MaPS, but a limitation we must live with. This means some operations which in
turn call the above routines, like installing packages, or expanding tarballs
will fail.

Fakeroot is a Linux program which intercepts calls to such operations, and when
instructed, instead of actually performing these operations, does a noop and
returns success to the calling code.

As a workaround to the namespace limitation, one can use fakeroot with the env
var FAKEROOTDONTTRYCHOWN set to '1', and successfully run otherwise troublesome
operations.

```bash
export FAKEROOTDONTTRYCHOWN='1'
fakeroot apt install openssh-client
```

## `--commit`

```bash
maps package -c <path-to-sandbox> runtime-specifier
```

```bash
maps package --commit <path-to-sandbox> runtime-specifier
```

This option turns your sandbox into a runtime. At this point, no more changes
should be made to the runtime, so, please make sure that everything is as you
want before you run this step.

The **runtime specifier** uniquely identifies a runtime to MaPS. It is of the
form `<software>/<platform>/<version>`. The `<software>` part of the identifier
needs to be in the reverse domain name notation. As an example, a valid
specifier is `org.oscar_system.oscar/x86_64/1.0.0`.

## `--upload`

```bash
maps package -u runtime-specifier
```

```bash
maps package --upload runtime-specifier
```

This option lets you upload your runtime onto the Official MaPS software
repository. To do this, you will require an authentication string, with a
limited time validity. This is to try to combat spam. Please contact us with
some information about who you are and what software you want to upload, and we
will provide you this authentication string. Once you have it, you need to
provide it to MaPS as an environment variable `MTDAUTH`, and MaPS will upload
your software to our servers. After a manual review, making sure everything is
in order, we will make your software available on the Official repository.

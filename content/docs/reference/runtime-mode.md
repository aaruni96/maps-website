---
title: "Runtime Mode"
description: "Reference pages are ideal for outlining how things work in terse
              and clear terms."
summary: ""
date: 2023-09-07T16:13:18+02:00
lastmod: 2023-09-07T16:13:18+02:00
draft: false
weight: 910
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

This is the default mode of the application, and is automatically selected when
no other mode is specified. In this mode, runtimes can be deployed, run,
updated, and uninstalled.

As of version 0.7, the following options are available :

```text
  --command COMMAND     Override for the command to run
  -d DEPLOY, --deploy DEPLOY
                        deploy mode, for installing environments
  -l, --list            List available environments
  --list-local          List available environments
  --repo REPO           Repository to use
  --reset RESET         Reset the runtime.
  -r RUN, --run RUN     Which runtime to play.
  -u UNINSTALL, --uninstall UNINSTALL
                        Uninstall a runtime
  --update UPDATE       Update a runtime
  --url URL             Deploy and launch a runtime from URL
  -v, --verbose         enable verbose output
  --no-gui              Disable GUI
  --gui                 Force enable GUI
  -e EXPORTURL, --export-url EXPORTURL
                        Export a runtime as a URL which maps can open
```

## A note on the runtime specifier

The __runtime specifier__ uniquely identifies a runtime to MaPS. It is of the
form `<software>/<platform>/<version>`. The `<software>` part of the identifier
needs to be in the [reverse domain name
notation](https://en.wikipedia.org/wiki/Reverse_domain_name_notation). As an
example, a valid specifier is `org.oscar_system.oscar/x86_64/1.0.0`.

A runtime specifier can be given in a "fully qualified" form, by including the
name of the remote repository in front of it. This helps disambiguate a runtime
if two runtimes of the same name are present in different repository. As an
example, a valid fully qualified specifier is
`Official:org.oscar_system.oscar/x86_64/1.0.0`.

If a fully qualified specifier is not provided, MaPS attempts to disambiguate
the runtime based on known information. If the runtime name is unique among all
known runtimes and all known remotes, the right remote is deduced. If this
disambiguation process fails, an error is reported and execution is halted.

## `--verbose`

Adding `-v` or `--verbose` to any command will run MaPS in verbose mode. This
prints a lot of extra information which might be helpful to investigate in case
things go wrong. Please include output in verbose mode whenever submitting a bug
report.

## `--list`

```bash
maps -l
```

```bash
maps --list
```

This option lists all available runtimes. The `Local` section lists runtimes
which have been packaged on the system, as well as runtimes which have been
installed on the system. The runtimes available from each remote repository are
listed in their individual systems.

## `--deploy`

```bash
maps -d <runtime-specifier>
```

```bash
maps --deploy <runtime-specifier>
```

This option deploys a runtime provided by the specifier. This will download the
the runtime from its remote to the system's repository, and deploy it to the
filesystem from where MaPS can use it. The download process is incremental. That
is, it can be aborted and resumed. In case of updates, only the files which are
updated on the remote need to be fetched.

### Telemetry

In case you enable the opt in telemetry, this is the only time MaPS will connect
to an external server to report telemetry. Only the following information is
transmitted :

- The name of the runtime being downloaded
- The name of the remote the runtime is being downloaded from
- The URL of the remote the runtime is being downloaded from In particular, no
personally identifiable information is collected. Username and password, if any,
are stripped from the remote runtime URL before transmission. IP addresses are
not logged.

## `--run`

```bash
maps -r <runtime-specifier>
```

```bash
maps --run <runtime-specifier>
```

This option executes a specified runtime. The runtime must already be deployed
before it can be run. As an overview, the following actions are performed :

1. A working directory for the runtime is setup, based on the read-only data
   published as the runtime, and any local changes saved onto a read-write layer
   above it.
2. The `$HOME/Public` directory from the host system is passed through to
   `/home/runtime/Public` inside the runtime.
3. The specified command from the manifest file is executed inside the runtime
   namespace.

    1. If there is no manifest file, or it does not specify a command, `bash` is
       executed.
    2. The command to launch can be overridden using the `--command` option.

## `--reset`

```bash
maps --reset <runtime-specifier>
```

This option removes any local changes from a deployed runtime. This "resets" the
runtime to only have content in it which was published in the remote repository.

## `--update`

```bash
maps -u <runtime-specifier>
```

```bash
maps --update <runtime-specifier>
```

This option updates a specified runtime. The runtime must already be deployed
before it can be updated. If no updates are available, this option will refresh
your deployed runtime, as if it has been deployed for the first time. This is
not the same as the above `--reset`, as this refresh operation will first remove
the deployed runtime, then freshly deploy it from the repository again.

## `--uninstall`

```bash
maps -u <runtime-specifier>
```

```bash
maps --uninstall <runtime-specifier>
```

This option uninstalls a specified runtime from your computer. It will first
remove the deployed copy of the runtime, and then proceed to delete the runtime
from your local repository. Trying to `--deploy` the runtime after this
operation will require you to re-download the runtime from a remote repository.

## `--export-url`

```bash
maps -e <runtime-specifier>
```

```bash
maps --export-url <runtime-specifier>
```

This option will generate a valid shareable URL of a MaPS runtime. This URL
allows a one-click workflow for deploying and running a runtime, if MaPS was
installed via your package manager. As an example, for OSCAR 1.0

```bash
maps --export-url org.oscar_system.oscar/x86_64/1.0.0
Generating a URL with the following info. Please check!
- Remote name is  Official
- Remote URL is   https://repo.oscar-system.org/
- Runtime is      org.oscar_system.oscar/x86_64/1.0.0

  maps://runtime?remotename=Official&remoteurl=https://repo.oscar-system.org/&runtime=org.oscar_system.oscar/x86_64/1.0.0
```

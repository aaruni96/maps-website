---
title: "Deploy and Run OSCAR"
description: ""
summary: ""
date: 2023-09-07T16:04:48+02:00
lastmod: 2023-09-07T16:04:48+02:00
draft: false
weight: 820
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

## Deploy OSCAR

Once MaPS is installed, deploying and running OSCAR is only two lines:

```bash
$ maps -d org.oscar_system.oscar/x86_64/latest
$ maps -r org.oscar_system.oscar/x86_64/latest
```

This will launch a shell inside the OSCAR runtime, and automatically launch
OSCAR from a pre built system image.

MaPS can also automatically deploy and launch runtimes from a URL (which MaPS
can be asked to export). For example, clicking on [this
link](maps://runtime?remotename=Official&remoteurl=https://repo.oscar-system.org/&runtime=org.oscar_system.oscar/x86_64/latest)
is equivalent to running the above two commands!

<script
  src="https://asciinema.org/a/suT9EW2hFK5291IloVeBO42wH.js"
  id="asciicast-suT9EW2hFK5291IloVeBO42wH"
  data-autoplay="true"
  async="true">
</script>

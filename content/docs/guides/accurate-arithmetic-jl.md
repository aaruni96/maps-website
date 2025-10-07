---
title: "Reproduce results from AccurateArithmetic.jl"
description: "tett tooot."
summary: ""
date: 2023-09-07T16:04:48+02:00
lastmod: 2023-09-07T16:04:48+02:00
draft: false
weight: 830
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

The [AccurateArithmetic.jl Julia
package](https://github.com/JuliaMath/AccurateArithmetic.jl/tree/paper-correctness-2019)
implements all algorithms described in [Accurate and Efficiently Vectorized Sums
and Dot Products in Julia (2019)](https://hal.science/hal-02265534). It also
contains everything needed to reproduce the results shown in the paper. Below is
a full list of the actions to be taken by anyone wanting to try and reproduce
the results on their own Linux system (adapted for MaPS from Appendix of the
linked paper)

Commands prefixed with a `sh>` prompt are to be entered in a shell; commands
prefixed with a `julia>` prompt are to be entered in a Julia interactive
session. The MaRDI Packaging System should have been downloaded and installed
beforehand from: https://github.com/aaruni96/maps

Be aware that step (3) in this procedure might take a few hours to complete.
Afterwards, all measurements should be available as JSON files in the
AccurateArithmetic.jl/test directory. After step (4), all figures showed in this
paper should be available as PDF files in the same directory.

1. Deploy and run the runtime

    ```bash
    maps -d org.juliamath.accuratearithmetic/x86_64/papercorrectnessv3
    maps -r org.juliamath.accuratearithmetic/x86_64/papercorrectnessv3
    ```

1. Start julia and run the test suite

    ```bash
    sh> cd /AccurateArithmetic.jl/test && julia --project
    julia> using Pkg
    julia> pkg"test"
    ```

1. Run the performance tests

    ```bash
    # Additional dependencies for performance tests.
    # Package testing fails if these are already included.
    julia> pkg"add BenchmarkTools Plots Printf Statistics Test"
    julia> exit()
    sh> julia --project -O3 -L perftests.jl -e ’run_tests()’
    ```

1. Plot the graphs

    ```bash
    sh> julia --project -L perfplorts.jl -e ’plot_results()’
    ```


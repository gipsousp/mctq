# mctq <a href = "https://docs.ropensci.org/mctq/"><img src = "man/figures/logo.png" align="right" height="139" /></a>

<!-- badges: start -->
[![Status at rOpenSci Software Peer
Review](https://badges.ropensci.org/434_status.svg)](https://github.com/ropensci/software-review/issues/434)
[![Repo
status](https://www.repostatus.org/badges/latest/active.svg)](https://www.repostatus.org/#active)
[![CRAN
status](https://www.r-pkg.org/badges/version/mctq)](https://cran.r-project.org/package=mctq)
[![CRAN
DOI](http://img.shields.io/badge/DOI-10.32614/CRAN.package.mctq-1284C5.svg)](https://doi.org/10.32614/CRAN.package.mctq)
[![CRAN
downloads](https://cranlogs.r-pkg.org/badges/grand-total/mctq)](https://danielvartan.shinyapps.io/cran-logs/?package=mctq)
[![R-universe](https://ropensci.r-universe.dev/badges/mctq)](https://ropensci.r-universe.dev)
[![Lifecycle:
maturing](https://img.shields.io/badge/lifecycle-maturing-blue.svg)](https://lifecycle.r-lib.org/articles/stages.html#maturing)
[![R-CMD-check](https://github.com/ropensci/mctq/workflows/R-CMD-check/badge.svg)](https://github.com/ropensci/mctq/actions)
[![Codecov test
coverage](https://codecov.io/gh/ropensci/mctq/branch/main/graph/badge.svg)](https://app.codecov.io/gh/ropensci/mctq?branch=main)
[![License:
MIT](https://img.shields.io/badge/license-MIT-green)](https://choosealicense.com/licenses/mit/)
[![fair-software.eu](https://img.shields.io/badge/fair--software.eu-%E2%97%8F%20%20%E2%97%8F%20%20%E2%97%8F%20%20%E2%97%8F%20%20%E2%97%8F-green)](https://fair-software.eu)
[![CII Best
Practices](https://bestpractices.coreinfrastructure.org/projects/6244/badge)](https://bestpractices.coreinfrastructure.org/projects/6244)
<!-- badges: end -->

## Overview

`mctq` is an R package that provides a complete toolkit to process the
Munich ChronoType Questionnaire (MCTQ), a quantitative and validated
tool to assess chronotypes using individuals’ sleep behavior, as
presented by Till Roenneberg, Anna Wirz-Justice, and Martha Merrow in
[2003](https://doi.org/10.1177/0748730402239679). Its aim is to
facilitate the work of sleep and chronobiology scientists with MCTQ data
and improve reproducibility in research.

`mctq` adheres to the [tidyverse
principles](https://tidyverse.tidyverse.org/articles/manifesto.html) and
integrates with the [tidyverse ecosystem](https://www.tidyverse.org/).

Learn more about the MCTQ questionnaire at
<https://www.thewep.org/documentations/mctq>.

### Why an R package for a questionnaire?

Although it may seem like a simple questionnaire, MCTQ requires
extensive date/time manipulation, which poses challenges for many
scientists. The `mctq` package addresses this issue by providing tools
to handle the processing tasks for the three MCTQ versions (standard,
micro, and shift) with few dependencies, relying mainly on the
[lubridate](https://lubridate.tidyverse.org/) and
[hms](https://hms.tidyverse.org/) packages from
[tidyverse](https://www.tidyverse.org/).

We designed `mctq` with user experience in mind, creating an interface
that resembles the questionnaire data as shown in MCTQ publications and
providing extensive documentation about each computation proposed by the
MCTQ authors. The package also includes fictional datasets for testing
and learning purposes.

## Prerequisites

You need some familiarity with the [R programming
language](https://www.r-project.org/) and the
[lubridate](https://lubridate.tidyverse.org/) and
[hms](https://hms.tidyverse.org/) packages from
[tidyverse](https://www.tidyverse.org/) to use `mctq`’s main functions.

If you are new to R, we recommend Hadley Wickham and Garrett Grolemund’s
free online book [R for Data Science](https://r4ds.hadley.nz/) and the
Coursera course from Johns Hopkins University [Data Science: Foundations
using
R](https://www.coursera.org/specializations/data-science-foundations-r)
(free for audit students).

Please refer to the [lubridate](https://lubridate.tidyverse.org/) and
[hms](https://hms.tidyverse.org/) documentation to learn more about
handling date/time data in R. We also recommend reading the [Dates and
times](https://r4ds.hadley.nz/datetimes) chapter from Wickham &
Grolemund’s book [R for Data Science](https://r4ds.hadley.nz/).

## Installation

You can install the released version of `mctq` from
[CRAN](https://CRAN.R-project.org/package=mctq) with:

``` r
install.packages("mctq")
```

And the development version from [GitHub](https://github.com/) with:

``` r
# install.packages("remotes")
remotes::install_github("ropensci/mctq")
```

## Usage

`mctq` uses the [lubridate](https://lubridate.tidyverse.org/) and
[hms](https://hms.tidyverse.org/) packages, which provide special
objects to handle date/time values in R. Ensure your dataset conforms to
this structure before using `mctq`. Refer to the respective package
documentation for more details.

Because of the [circular nature of time](https://youtu.be/eelVqfm8vVc),
using appropriate temporal objects is crucial to avoid computation
mistakes while adapting data from a base 10 to a base 12 numerical
system.

For detailed usage instructions, visit our [Get started
guide](https://docs.ropensci.org/mctq/articles/mctq.html).

### Workdays and work-free days variables

After preparing your data, use the following `mctq` functions to process
it. The function names follow the patterns used in MCTQ publications,
making it easy to apply the necessary computations:

- `fd()`: compute MCTQ work-free days.
- `so()`: compute MCTQ local time of sleep onset.
- `gu()`: compute MCTQ local time of getting out of bed.
- `sdu()`: compute MCTQ sleep duration.
- `tbt()`: compute MCTQ total time in bed.
- `msl()`: compute MCTQ local time of mid-sleep.
- `napd()`: compute MCTQ nap duration (only for MCTQ Shift).
- `sd24()`: compute MCTQ 24 hours sleep duration (only for MCTQ Shift).

Example:

``` r
# Local time of preparing to sleep on workdays
sprep_w <- c(hms::parse_hm("23:45"), hms::parse_hm("02:15"))
# Sleep latency or time to fall asleep after preparing to sleep on workdays
slat_w <- c(lubridate::dminutes(30), lubridate::dminutes(90))
# Local time of sleep onset on workdays
so(sprep_w, slat_w)
```

    00:15:00
    03:45:00

### Combining workdays and work-free days variables

For computations combining workdays and work-free days, use:

- `sd_week()`: compute MCTQ average weekly sleep duration.
- `sd_overall()`: compute MCTQ overall sleep duration (only for MCTQ
  Shift).
- `sloss_week()`: compute MCTQ weekly sleep loss.
- `le_week()`: compute MCTQ average weekly light exposure.
- `msf_sc()`: compute MCTQ chronotype or sleep-corrected local time of
  mid-sleep on work-free days.
- `sjl()` and `sjl_rel()`: compute MCTQ social jet lag.
- `sjl_sc()` and `sjl_sc_rel()`: compute Jankowski’s MCTQ
  sleep-corrected social jetlag.
- `sjl_weighted()`: compute MCTQ absolute social jetlag across all
  shifts (only for MCTQ Shift).

Example:

``` r
# Local time of mid-sleep on workdays
msw <- c(hms::parse_hm("02:05"), hms::parse_hm("04:05"))
# Local time of mid-sleep on work-free days
msf <- c(hms::parse_hm("23:05"), hms::parse_hm("08:30"))
# Relative social jetlag
sjl_rel(msw, msf)
```

    [1] "-10800s (~-3 hours)"  "15900s (~4.42 hours)"

### Utilities

`mctq` includes utility tools to help with your MCTQ data and provides
fictional datasets for the standard, micro, and shift MCTQ versions for
testing and learning purposes.

All functions are documented with guidelines behind the computations.
Click [here](https://docs.ropensci.org/mctq/reference/index.html) to see
the full list.

## Citation

If you use `mctq` in your research, please consider citing it. We put
significant effort into building and maintaining this free and
open-source R package. Find the citation below.

``` r
citation("mctq")
```

    To cite {mctq} in publications use:

      Vartanian, D. (2025). {mctq}: Munich ChronoType Questionnaire tools
      (Version 0.3.2.9001) [Computer software - R package]. CRAN; rOpenSci.
      https://doi.org/10.32614/CRAN.package.mctq

    A BibTeX entry for LaTeX users is

      @Misc{,
        title = {{mctq}: Munich ChronoType Questionnaire tools},
        author = {Daniel Vartanian},
        year = {2025},
        publisher = {CRAN; rOpenSci},
        doi = {10.32614/CRAN.package.mctq},
        note = {R package version 0.3.2.9001},
      }

## Contributing

We welcome contributions, including bug reports. Take a moment to review
our [Guidelines for
Contributing](https://docs.ropensci.org/mctq/CONTRIBUTING.html).

## Acknowledgments

The initial development of `mctq` was supported by a scholarship from
the [University of Sao Paulo (USP)](http://usp.br/) (❤️).

The `mctq` hex logo is based on an illustration by [hilda design matters
Zurich](https://hilda.ch/) for the [Daylight Academy
(DLA)](https://daylight.academy/).

<br>

Become an `mctq` supporter!

Click [here](https://github.com/sponsors/danielvartan) to make a
donation. Please indicate the `mctq` package in your donation message.

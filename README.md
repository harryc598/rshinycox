
<!-- README.md is generated from README.Rmd. Please edit that file -->

# rshinycox

The goal of rshinycox is to create a shiny app that displays a predicted
survival curve or multiple curves. The motivation for this is multifold:
for one, shiny apps are excellent tools for visualization, but are not
always a straightforward process. This package allows the statistician
to input their finished Cox models into the function `shine_coxph()` and
it will create a shiny app for the user, with no other work required.
The other motivation was to create an app that contained none of the
original data used to create the Cox models. With this requirement,
there is no worry of disclosing private data. So `shine_coxph()` will
use the data for verification purposes, but discard it when the app is
made, containing only the bare necessities to make predictions.

## Installation

You can install the development version of rshinycox from
[GitHub](https://github.com/) with:

``` r
# install.packages("devtools")
devtools::install_github("harryc598/rshinycox")
```

## Example

Here is an example using multiple treatment arms, which will highlight
the usefulness of this package. If you move around the inputs, you can
see how for different combinations, one treatment might prevail over the
other.

``` r
library(rshinycox)
library(survival)
split_colon <- split(colon, colon$rx)

colon_arm1 <- split_colon$Obs
colon_arm2 <- split_colon$Lev
colon_arm3 <- split_colon$`Lev+5FU`

colon1ph <- coxph(Surv(time, status) ~sex +  age + obstruct + nodes, colon_arm1,
                  x = TRUE, model = TRUE)
colon2ph <- coxph(Surv(time, status) ~ sex + age + obstruct + nodes, colon_arm2,
                  x = TRUE, model = TRUE)
colon3ph <- coxph(Surv(time, status) ~ sex + age + obstruct + nodes, colon_arm3,
                  x = TRUE, model = TRUE)
# This will write a shiny app into whatever your working directory is
# shine_coxph("arm1" = colon1ph, "arm2" = colon2ph, "arm3" = colon3ph, theme = "dashboard", app.dir = getwd())
```

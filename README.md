
<!-- README.md is generated from README.Rmd. Please edit that file -->

# BTtest

<!-- badges: start -->
<!-- [![CRAN\_Version\_Badge](http://www.r-pkg.org/badges/version/BTtest)](https://cran.r-project.org/package=BTtest) -->
<!-- [![CRAN\_Downloads\_Badge](https://cranlogs.r-pkg.org/badges/grand-total/BTtest)](https://cran.r-project.org/package=BTtest) -->

[![R-CMD-check](https://github.com/Paul-Haimerl/BTtest/actions/workflows/R-CMD-check.yaml/badge.svg)](https://github.com/Paul-Haimerl/BTtest/actions/workflows/R-CMD-check.yaml)
<!-- badges: end -->

Conveniently test for the number of common factors in large
nonstationary panels using the routine by Barigozzi & Trapani
([2022](https://doi.org/10.1080/07350015.2021.1901719)).

## Installation

You can install the development version of BTtest from
[GitHub](https://github.com/) with:

``` r
# install.packages("devtools")
devtools::install_github("Paul-Haimerl/BTtest")
```

After installation, attach the package as usual:

``` r
library(BTtest)
```

## Data

The `BTtest` packages includes a function that automatically simulates a
panel with common nonstationary trends:

``` r
# Simulate a DGP containing a factor with a linear drift (r1, d1 = 1 -> drift = TRUE) and I(1) process 
# (d2 = 1 -> drift_I1 = TRUE), one zero-mean I(1) factor (r2 = 1 -> r_I1 = 2; since drift_I1 = TRUE) 
# and two zero-mean I(0) factors (r3 = 2 -> r_I0 = 2)
X <- sim_DGP(N = 100, n_Periods = 200, drift = TRUE, drift_I1 = TRUE, r_I1 = 2, r_I0 = 2)
```

For specifics on the DGP, I refer to Barigozzi & Trapani
([2022](https://doi.org/10.1080/07350015.2021.1901719), sec. 5).

## The Barigozzi & Trapani ([2022](https://doi.org/10.1080/07350015.2021.1901719)) test

To run the test, the user only needs to pass a $T \times N$ data matrix
`X` and specify an upper limit on the number of factors (`r_max`), a
significance level (`alpha`) and whether to use a less (`BT1 = TRUE`) or
more conservative (`BT1 = FALSE`) eigenvalue scaling scheme:

``` r
BTtest(X = X, r_max = 10, alpha = 0.05, BT1 = TRUE)
```

Differences between `BT1 = TRUE/ FALSE`, where `BT1 = TRUE` tends to
identify more factors compared to `BT1 = FALSE`, quickly vanish when the
panel includes more than 200 time periods ([Barigozzi & Trapani
2022](https://doi.org/10.1080/07350015.2021.1901719), sec. 5; [Trapani,
2018](https://doi.org/10.1080/01621459.2017.1328359), sec. 3).

## The Bai ([2004](https://doi.org/10.1016/j.jeconom.2003.10.022)) Integrated Information Criterion

An alternative way of estimating the number of factors in a
nonstationary panel is the Integrated Information Criterion by Bai
([2004](https://doi.org/10.1016/j.jeconom.2003.10.022)). The package
also contains a function to easily evaluate this measure:

``` r
BaiIPC(X = X, r_max = 10)
```

## References

- Bai, J. (2004). Estimating cross-section common stochastic trends in
  nonstationary panel data. *Journal of Econometrics*, 122(1), 137-183.
  DOI:
  [10.1016/j.jeconom.2003.10.022](https://doi.org/10.1016/j.jeconom.2003.10.022)
- Barigozzi, M., & Trapani, L. (2022). Testing for common trends in
  nonstationary large datasets. *Journal of Business & Economic
  Statistics*, 40(3), 1107-1122. DOI:
  [10.1080/07350015.2021.1901719](https://doi.org/10.1080/07350015.2021.1901719)
- Trapani, L. (2018). A randomized sequential procedure to determine the
  number of factors. *Journal of the American Statistical Association*,
  113(523), 1341-1349. DOI:
  [10.1080/01621459.2017.1328359](https://doi.org/10.1080/01621459.2017.1328359)

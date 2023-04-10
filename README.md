
<!-- README.md is generated from README.Rmd. Please edit that file -->
<style type="text/css">
.codeblock-label {
  color: #000;
  display: inline-block;
  border-top-left-radius: .5rem;
  border-top-right-radius: .5rem;
  padding: 0.25rem 0.75rem;
  background-color: #cccccc;
  margin-bottom: 0;
  font-size: 0.875em;
  font-family: var(--bs-font-monospace);
}
  
.codeblock-label + div.sourceCode {
  margin-top: 0;
}
</style>

# config <img src='man/figures/logo.svg' align="right" height="139" />

<!-- badges: start -->

[![CRAN
status](https://www.r-pkg.org/badges/version/config)](https://CRAN.R-project.org/package=config)
[![R-CMD-check](https://github.com/rstudio/config/workflows/R-CMD-check/badge.svg)](https://github.com/rstudio/config/actions)
[![Codecov test
coverage](https://codecov.io/gh/rstudio/config/branch/main/graph/badge.svg)](https://app.codecov.io/gh/rstudio/config?branch=main)
<!-- badges: end -->

The `config` package makes it easy to manage environment specific
configuration values. For example, you might want to use distinct values
for development, testing, and production environments.

## Installation

You can install the `config` package from CRAN by using:

``` r
install.packages("config")
```

## Usage

To use `config`, create a file `config.yml` with default as well as
other arbitrary configurations. For example:

<p class="codeblock-label">
config.yml
</p>

``` yaml
default:
  trials: 5
  dataset: "data-sampled.csv"
  
production:
  trials: 30
  dataset: "data.csv"
```

To read configuration values you call the `config::get` function, which
returns a list containing all of the values for the currently active
configuration:

``` r
config <- config::get()
config$trials
config$dataset
```

You can also read a single value from the configuration as follows:

``` r
config::get("trials")
config::get("dataset")
```

The `config::get()` function takes an optional `config` argument which
determines which configuration to read values from (the “default”
configuration is used if none is specified).

## Do not attach the package using `libary(config)`

We strongly recommend you use `config::get()` rather than attaching the
package using `library(config)`.

In fact, we strongly recommend you never use `library(config)`.

The underlying reason is that the `get()` and `merge()` functions in
`{config}` will mask these functions with the same names in base R.

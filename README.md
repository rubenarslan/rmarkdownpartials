
<!-- README.md is generated from README.Rmd. Please edit that file -->

# rmdpartials

[![Travis-CI Build
Status](https://travis-ci.org/rubenarslan/rmdpartials.svg?branch=master)](https://travis-ci.org/rubenarslan/rmdpartials)
[![codecov](https://codecov.io/gh/rubenarslan/rmdpartials/branch/master/graph/badge.svg)](https://codecov.io/gh/rubenarslan/rmdpartials)

*Simplify using rmarkdown partials to document objects in R*

## Description

Ever want to make a standardized way to report a summary of something
like a regression, but did not want to limit yourself to one unformatted
block of text, one table, or one figure?

Rmarkdown partials allow you to define standardised knitr code chunks
that become part of your rmarkdown report. They can then be turned into
HTML, PDFs, or Word files. You could, for example, create an rmarkdown
partial to summarise regression models in a flexible way.

You can also define your partials as methods of `knit_print`, so that a
rich rmarkdown partial is made by default.

## Documentation

Confer the help or: <https://rubenarslan.github.io/rmdpartials>. See the
[vignette](https://rubenarslan.github.io/rmdpartials/articles/rmdpartials.html)
for a quick example of an HTML document generated with `rmdpartials`.

## Install

To get the latest development version:

``` r
install.packages("remotes")
remotes::install_github("rubenarslan/rmdpartials")
```

## Define a partial

Define a function like this:

``` r
my_summary <- function(object) {
  rmdpartials::partial("_my_summary.Rmd")
}
```

And create a file called `_my_summary.Rmd` with contents like this:

    ## My special summary
    
    ```{r}
    summary(object)
    ```
    
    ## My special plot
    ```{r}
    plot(object)
    ```

## Usage

To use the partial in an rmarkdown report

    ```{r}
    m1 <- lm(y ~ x, data = data)
    my_summary(m1)
    ```

### Usage as a knit\_print method

To make your partial the default printing option for objects of a
certain class when they are echoed in a knitr document, give it the name
of a knit\_print method.

``` r
knit_print.lm <- function(object) {
  rmdpartials::partial("_my_summary.Rmd")
}
```

Now, all you need to is let the lm object be echoed.

    ```{r}
    m1 <- lm(y ~ x, data = data)
    m1
    ```

You can also preview what the result from the partial would look like by
calling it in an interactive
session.

## [Code of conduct for contributing](https://rubenarslan.github.io/rmdpartials/CONDUCT.html)

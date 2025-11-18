
<!-- README.md is generated from README.Rmd. Please edit that file -->

# missingGroupr Package

<!-- badges: start -->
<!-- badges: end -->

The goal of missingGroupr is to provide a helper function that
summarizes the number of missing values in all the columns when grouped
by a specified column. The function wraps `dplyr::group_by()`,
`dplyr::summarize()`, and `dplyr::across()` to compute missing-value
counts.

## Installation

You can install the development version of missingGroupr from
[GitHub](https://github.com/stat545ubc-2025/missingGroupr) with:

``` r
# install.packages("devtools")
devtools::install_github("stat545ubc-2025/missingGroupr")
```

## Examples

This example computes the number of missing values in the `airquality`
dataset grouped by the `Month` column.

``` r
missingGroupr::count_all_missing_by_group(airquality, Month)
#> # A tibble: 5 × 6
#>   Month Ozone Solar.R  Wind  Temp   Day
#>   <int> <int>   <int> <int> <int> <int>
#> 1     5     5       4     0     0     0
#> 2     6    21       0     0     0     0
#> 3     7     5       0     0     0     0
#> 4     8     5       3     0     0     0
#> 5     9     1       0     0     0     0
```

This example has the same output as the last example, but shows off an
alternative way of invoking the `count_all_missing_by_group()`: piping
the dataset into the function.

``` r
airquality |> missingGroupr::count_all_missing_by_group(Month) 
#> # A tibble: 5 × 6
#>   Month Ozone Solar.R  Wind  Temp   Day
#>   <int> <int>   <int> <int> <int> <int>
#> 1     5     5       4     0     0     0
#> 2     6    21       0     0     0     0
#> 3     7     5       0     0     0     0
#> 4     8     5       3     0     0     0
#> 5     9     1       0     0     0     0
```

The optional `.groups` argument allows us to keep the output grouped by
the grouping column. See example below; notice how the output is a
grouped tibble, rather than the ungrouped tibble output of the earlier
examples.

``` r
missingGroupr::count_all_missing_by_group(airquality, Month, .groups = "keep")
#> # A tibble: 5 × 6
#> # Groups:   Month [5]
#>   Month Ozone Solar.R  Wind  Temp   Day
#>   <int> <int>   <int> <int> <int> <int>
#> 1     5     5       4     0     0     0
#> 2     6    21       0     0     0     0
#> 3     7     5       0     0     0     0
#> 4     8     5       3     0     0     0
#> 5     9     1       0     0     0     0
```

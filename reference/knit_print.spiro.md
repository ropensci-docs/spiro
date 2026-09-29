# Printing spiro data frames in a knitr context

`knit_print.spiro()` provides a method for printing `data.frames` from
[`spiro`](https://docs.ropensci.org/spiro/reference/spiro.md) within
`knitr`.

## Usage

``` r
# S3 method for class 'spiro'
knit_print(x, min = 10, max = 20, digits = 2, ...)
```

## Arguments

- x:

  A `data.frame` of the class `spiro` to be printed.

- min:

  An integer, which sets the number of rows to which `x` will be limited
  in printing if row number exceed `max`.

- max:

  An integer, setting the maximal number of rows to be not cut to `min`
  in printing.

- digits:

  An integer giving the number of decimals to be rounded to.

- ...:

  Passing of additional arguments to `knit_print.default()`.

## Value

The function prints its argument and returns it invisibly.

## Details

Cardiopulmonary exercise testing data imported by
[`spiro`](https://docs.ropensci.org/spiro/reference/spiro.md) will often
come in large `data.frame`s. When knitting R Markdown documents these
will normally be printed in full size.

This function provides a method for `data.frame`s of the class `spiro`
to limit the number of rows displayed to `min` if it exceeds `max`. The
number of hidden data rows will be printed below the `data.frame`.

## Examples

``` r
# Get example data
s <- spiro(spiro_example("zan_gxt"))

knitr::knit_print(s)
#>    load step time    VO2   VCO2    RR   VT    VE HR PetO2 PetCO2 VO2_rel
#> 1     0    0    1     NA     NA    NA   NA    NA NA    NA     NA      NA
#> 2     0    0    2     NA     NA    NA   NA    NA NA    NA     NA      NA
#> 3     0    0    3     NA     NA    NA   NA    NA NA    NA     NA      NA
#> 4     0    0    4 399.08 323.70 13.94 0.77 10.72 NA    NA     NA    6.05
#> 5     0    0    5 409.83 330.26 14.50 0.74 10.66 NA    NA     NA    6.21
#> 6     0    0    6 420.58 336.82 15.06 0.71 10.60 NA    NA     NA    6.37
#> 7     0    0    7 431.33 343.37 15.63 0.68 10.53 NA    NA     NA    6.54
#> 8     0    0    8 435.30 346.51 16.06 0.69 11.04 NA    NA     NA    6.60
#> 9     0    0    9 437.02 348.52 16.46 0.71 11.74 NA    NA     NA    6.62
#> 10    0    0   10 438.74 350.53 16.85 0.74 12.44 NA    NA     NA    6.65
#>    VCO2_rel RE  RER  CHO   FO
#> 1        NA NA   NA   NA   NA
#> 2        NA NA   NA   NA   NA
#> 3        NA NA   NA   NA   NA
#> 4      4.90 NA 0.81 0.20 0.13
#> 5      5.00 NA 0.81 0.19 0.13
#> 6      5.10 NA 0.80 0.19 0.14
#> 7      5.20 NA 0.80 0.18 0.15
#> 8      5.25 NA 0.80 0.18 0.15
#> 9      5.28 NA 0.80 0.19 0.15
#> 10     5.31 NA 0.80 0.19 0.15
#> $load
#>  [1] 0 0 0 0 0 0 0 0 0 0
#> 
#> $step
#>  [1] 0 0 0 0 0 0 0 0 0 0
#> 
#> $time
#>  [1]  1  2  3  4  5  6  7  8  9 10
#> 
#> $VO2
#>  [1]     NA     NA     NA 399.08 409.83 420.58 431.33 435.30 437.02 438.74
#> 
#> $VCO2
#>  [1]     NA     NA     NA 323.70 330.26 336.82 343.37 346.51 348.52 350.53
#> 
#> $RR
#>  [1]    NA    NA    NA 13.94 14.50 15.06 15.63 16.06 16.46 16.85
#> 
#> $VT
#>  [1]   NA   NA   NA 0.77 0.74 0.71 0.68 0.69 0.71 0.74
#> 
#> $VE
#>  [1]    NA    NA    NA 10.72 10.66 10.60 10.53 11.04 11.74 12.44
#> 
#> $HR
#>  [1] NA NA NA NA NA NA NA NA NA NA
#> 
#> $PetO2
#>  [1] NA NA NA NA NA NA NA NA NA NA
#> 
#> $PetCO2
#>  [1] NA NA NA NA NA NA NA NA NA NA
#> 
#> $VO2_rel
#>  [1]   NA   NA   NA 6.05 6.21 6.37 6.54 6.60 6.62 6.65
#> 
#> $VCO2_rel
#>  [1]   NA   NA   NA 4.90 5.00 5.10 5.20 5.25 5.28 5.31
#> 
#> $RE
#>  [1] NA NA NA NA NA NA NA NA NA NA
#> 
#> $RER
#>  [1]   NA   NA   NA 0.81 0.81 0.80 0.80 0.80 0.80 0.80
#> 
#> $CHO
#>  [1]   NA   NA   NA 0.20 0.19 0.19 0.18 0.18 0.19 0.19
#> 
#> $FO
#>  [1]   NA   NA   NA 0.13 0.13 0.14 0.15 0.15 0.15 0.15
#> 
#> [[18]]
#> [1] "... with 2999 more rows"
#> 
```

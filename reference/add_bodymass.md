# Calculate additional variables related to body mass for cardiopulmonary exercise testing data

`add_bodymass()` adds body mass-related variables to processed gas
exchange data.

## Usage

``` r
add_bodymass(data, bodymass = NULL)
```

## Arguments

- data:

  A `data.frame` of the class `spiro` containing the gas exchange data.
  Usually the output of a
  [`spiro`](https://docs.ropensci.org/spiro/reference/spiro.md) call.

- bodymass:

  A numeric value to manually set the participant's body mass. Defaults
  to NULL to use body mass data from the file's meta data. Set to NA to
  ignore the meta data without setting a new body mass.

## Value

A `data.frame` of the class `spiro` containing the cardiopulmonary
exercise testing data including variables related to body mass.

## Details

Based on an individual's body mass, relative oxygen uptake (VO2_rel) and
carbon dioxide output (VCO2_rel) are calculated. For running protocols,
running economy (RE) is calculated.

## Examples

``` r
# get example file
file <- spiro_example("zan_gxt")

s <- spiro(file)
out <- add_bodymass(s, bodymass = 65.3)
head(out)
#>   load step time    VO2   VCO2    RR   VT    VE HR PetO2 PetCO2 VO2_rel
#> 1    0    0    1     NA     NA    NA   NA    NA NA    NA     NA      NA
#> 2    0    0    2     NA     NA    NA   NA    NA NA    NA     NA      NA
#> 3    0    0    3     NA     NA    NA   NA    NA NA    NA     NA      NA
#> 4    0    0    4 399.08 323.70 13.94 0.77 10.72 NA    NA     NA    6.11
#> 5    0    0    5 409.83 330.26 14.50 0.74 10.66 NA    NA     NA    6.28
#> 6    0    0    6 420.58 336.82 15.06 0.71 10.60 NA    NA     NA    6.44
#>   VCO2_rel RE  RER  CHO   FO
#> 1       NA NA   NA   NA   NA
#> 2       NA NA   NA   NA   NA
#> 3       NA NA   NA   NA   NA
#> 4     4.96 NA 0.81 0.20 0.13
#> 5     5.06 NA 0.81 0.19 0.13
#> 6     5.16 NA 0.80 0.19 0.14
```

# Import and add heart rate data to cardiopulmonary exercise testing data

`add_hr()` imports an external file containing heart rate data and adds
it to an existing gas exchange data file.

## Usage

``` r
add_hr(data, hr_file, hr_offset = 0)
```

## Arguments

- data:

  A `data.frame` of the class `spiro` containing the gas exchange data.
  Usually the output of a
  [`spiro`](https://docs.ropensci.org/spiro/reference/spiro.md) call.

- hr_file:

  The absolute or relative path of a `*tcx` file that contains
  additional heart rate data.

- hr_offset:

  An integer, corresponding to the temporal offset of the heart-rate
  file. By default the start of the heart rate measurement is linked to
  the start of the gas exchange measurement. A positive value means,
  that the heart rate measurement started after the begin of the gas
  exchange measurements; a negative value means it started before.

## Value

A `data.frame` of the class `spiro` containing the cardiopulmonary
exercise testing data including heart rate data.

## Details

Heart rate data will be imported from a `.tcx` file. After interpolating
the data to full seconds, it is then matched to the imported gas
exchange data.

## Examples

``` r
# Get example data
oxy_file <- spiro_example("zan_ramp")
hr_file <- spiro_example("hr_ramp.tcx")

# Import and process spiro data
oxy_data <- spiro(oxy_file)

# Add heart rate data
out <- add_hr(oxy_data, hr_file)
head(out)
#>   load step time    VO2   VCO2    RR   VT    VE  HR PetO2 PetCO2 VO2_rel
#> 1    0    0    1 563.56 551.23 21.66 0.74 15.88 127    NA     NA    8.54
#> 2    0    0    2 604.44 593.12 21.00 0.81 16.90 126    NA     NA    9.16
#> 3    0    0    3 645.33 635.01 20.33 0.88 17.92 125    NA     NA    9.78
#> 4    0    0    4 633.98 627.16 19.28 0.94 18.06 125    NA     NA    9.61
#> 5    0    0    5 599.17 596.96 18.06 1.00 17.80 122    NA     NA    9.08
#> 6    0    0    6 564.36 566.76 16.83 1.06 17.55 119    NA     NA    8.55
#>   VCO2_rel RE  RER  CHO   FO
#> 1     8.35 NA 0.98 0.71 0.02
#> 2     8.99 NA 0.98 0.77 0.02
#> 3     9.62 NA 0.98 0.83 0.01
#> 4     9.50 NA 0.99 0.83 0.01
#> 5     9.04 NA 1.00 0.80 0.00
#> 6     8.59 NA 1.00 0.78 0.00
```

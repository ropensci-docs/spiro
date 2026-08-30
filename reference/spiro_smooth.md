# Apply a smoothing filter to data from cardiopulmonary exercise testing.

Filter vectors and data frames with moving averages and digital filters.
Provides the data filtering for
[`spiro_max`](https://docs.ropensci.org/spiro/reference/spiro_max.md)
and
[`spiro_plot`](https://docs.ropensci.org/spiro/reference/spiro_plot.md).

## Usage

``` r
spiro_smooth(data, smooth = 30, columns = NULL, quiet = FALSE)
```

## Arguments

- data:

  A data frame of the class `spiro`. Usually the output of the
  [`spiro`](https://docs.ropensci.org/spiro/reference/spiro.md)` function`.

- smooth:

  An integer or character string specifying the smoothing strategy and
  parameters. Default is `30`, which means the applied filter is a
  30-second moving average. See the section **'Filtering Methods'** for
  more details.

- columns:

  A character vector of the data columns that should be filtered. By
  default the filtering applies to all data column of `data` (besides
  load, time and step).

- quiet:

  Whether warning message should be suppressed. Default is FALSE.

## Value

A data frame

## Details

Raw data from cardiopulmonary is usually noisy due to measurement error
and biological breath-to-breath variability. When processing or
visualizing the gas exchange data, it is often helpful to filter the raw
data. This function provides different filtering methods (time average,
breath average, digital filters).

Breath-based and digital filters will be applied on the raw
breath-by-breath data. Time-based averages will be used on the
interpolated data.

## Filtering Methods

- Time-Based Average (e.g. `smooth = 30`):

  A (centered) moving average over a defined time span. The number can
  be given as an integer or as a character (e.g. `smooth = "30"`) and
  defines the length of the calculation interval in seconds.

- Breath-Based Average (e.g. `smooth = "15b"`):

  A (centered) moving average over a defined number of breaths. The
  integer before the letter 'b' defines the number of breaths for the
  calculation interval.

- Butterworth filter (e.g. `smooth = "0.04f3"`):

  A digital Butterworth filter (with lag). The number before the letter
  'f' defines the low-pass cut-off frequency, the number after the
  letter 'f' gives the order of the filter. See
  [`bw_filter`](https://docs.ropensci.org/spiro/reference/bw_filter.md)
  for more details.

- Zero-lag Butterworth filter (e.g. `smooth = "0.04fz3"`):

  A digital forwards-backwards Butterworth filter (without lag). The
  number before the letter 'f' defines the low-pass cut-off frequency,
  the number after gives the order of the filter. See
  [`bw_filter`](https://docs.ropensci.org/spiro/reference/bw_filter.md)
  for more details.

## Examples

``` r
# Get example data
file <- spiro_example("zan_gxt")
d <- spiro(file)

out <- spiro_smooth(d, 30)
head(out)
#>   VO2 VCO2 RR VT VE HR PetO2 PetCO2 VO2_rel VCO2_rel RE RER CHO FO
#> 1  NA   NA NA NA NA NA    NA     NA      NA       NA NA  NA  NA NA
#> 2  NA   NA NA NA NA NA    NA     NA      NA       NA NA  NA  NA NA
#> 3  NA   NA NA NA NA NA    NA     NA      NA       NA NA  NA  NA NA
#> 4  NA   NA NA NA NA NA    NA     NA      NA       NA NA  NA  NA NA
#> 5  NA   NA NA NA NA NA    NA     NA      NA       NA NA  NA  NA NA
#> 6  NA   NA NA NA NA NA    NA     NA      NA       NA NA  NA  NA NA

# filter only the VO2 column with a zero-phase Butterworth filter
out2 <- spiro_smooth(d, "0.04fz3", columns = "VO2")
head(out2)
#>        VO2
#> 1 398.2345
#> 2 400.9441
#> 3 406.3668
#> 4 414.5101
#> 5 425.3846
#> 6 439.0040
```

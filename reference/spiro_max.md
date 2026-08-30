# Return maximum values from cardiopulmonary exercise tests

`spiro_max()` returns a `data.frame` with the maximum gas exchange
parameters of an exercise test.

## Usage

``` r
spiro_max(data, smooth = 30, hr_smooth = FALSE)
```

## Arguments

- data:

  A `data.frame` of the class `spiro` containing the gas exchange data.
  Usually the output of a
  [`spiro`](https://docs.ropensci.org/spiro/reference/spiro.md) call.

- smooth:

  Parameter giving the filter methods for smoothing the data. Default is
  `30` for a 30-second moving average. `"20b"` will apply a 20-breath
  averaging for example. See
  [`spiro_smooth`](https://docs.ropensci.org/spiro/reference/spiro_smooth.md)
  for further details and filter methods (e.g. Butterworth filters).

- hr_smooth:

  A logical, whether smoothing should also apply to heart rate data.
  Default is `FALSE`, which means that the absolute maximum heart rate
  value is taken without smoothing.

## Value

A `data.frame` with the maximum parameter values of the data.

## Details

Before calculating the maximum values, the raw data is smoothed. Default
smoothing method is a 30-second rolling average. See the `smooth`
argument in
[`spiro_smooth`](https://docs.ropensci.org/spiro/reference/spiro_smooth.md)
for more options, such as breath-based averages or digital filtering.

Parameters calculated are the maxima of oxygen uptake (absolute and
relative), carbon dioxide output, minute ventilation, respiratory
exchange ratio (RER), and heart rate. The maximum values are defined as
the highest single data values after the smoothing.

For the maximum RER a different algorithm is used, as the RER during and
after rest may exceed the peak value during exercise. Therefore only
values during the last ten percent of the exercise time are considered
for the RERmax determination. The RERmax calculation works best for data
from tests without rest intervals (e.g., ramp tests) and with attached
load protocol data.

## Examples

``` r
# Import and process example data sets
gxt_data <- spiro(file = spiro_example("zan_gxt"))

spiro_max(gxt_data)
#>       VO2    VCO2     VE VO2_rel  RER HR
#> 1 4732.28 4640.75 129.62    71.7 0.99 NA

# Use an averaging over a time interval of 15 seconds
spiro_max(gxt_data, smooth = 15)
#>      VO2    VCO2     VE VO2_rel  RER HR
#> 1 4774.6 4681.83 130.56   72.34 1.02 NA

# Use an averaging over an interval of 15 breaths
spiro_max(gxt_data, smooth = "15b")
#>       VO2   VCO2     VE VO2_rel  RER HR
#> 1 4774.13 4674.8 130.79   72.34 1.02 NA
```

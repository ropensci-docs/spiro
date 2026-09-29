# Smooth data with a (zero-phase) Butterworth filter

Internal function for
[`spiro_smooth`](https://docs.ropensci.org/spiro/reference/spiro_smooth.md).

## Usage

``` r
bw_filter(x, n = 3, W = 0.04, zero_lag = TRUE)
```

## Arguments

- x:

  A numeric vector on which the digital filter should be applied

- n:

  Order of the Butterworth filter, defaults to 3

- W:

  Low-pass cut-off frequency of the filter, defaults to 0.04

- zero_lag:

  Whether a zero phase (forwards-backwards) filter should be applied.

## Value

A numeric vector of the same length as x.

## Details

Digital filtering might be a preferable processing strategy for
smoothing data from gas exchange measures when compared to moving
averages. Robergs et al. (2010) proposes a third order Butterworth
filter with a low-pass cut-off frequency of 0.04 for filtering VO2 data.

It should be noted that Butterworth filter comprise a time lag. A method
to create a time series with zero lag is to subsequently apply two
Butterworth filters in forward and reverse direction (forwards-backwards
filtering). While this procedure removes any time lag it changes the
magnitude of the filtering response, i.e. the resulting filter has not
the same properties (order and cut-off frequency) as a single filter.

## Examples

``` r
# Get VO2 data from example file
vo2_vector <- spiro(spiro_example("zan_gxt"))$VO2

out <- bw_filter(vo2_vector)
head(out, n = 20)
#>  [1]       NA       NA       NA 506.5931 509.6280 513.2645 517.4021 521.9252
#>  [9] 526.7046 531.6010 536.4678 541.1546 545.5111 549.3910 552.6563 555.1817
#> [17] 556.8583 557.5975 557.3338 556.0264
```

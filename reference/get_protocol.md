# Guess a test protocol from a corresponding exercise testing data set

`get_protocol()` gets the underlying test protocol based on given load
data.

## Usage

``` r
get_protocol(data)
```

## Arguments

- data:

  A `data.frame` containing the exercise testing data. It is highly
  recommend to parse non-interpolated breath-by-breath data or processed
  data with a very short interpolating/averaging interval.

## Value

A `data.frame` with the duration and load of each protocol step.

## Examples

``` r
# Import example data
raw_data <- spiro_raw(data = spiro_example("zan_gxt"))

get_protocol(raw_data)
#>    duration load
#> 1        60  0.0
#> 2       300  2.0
#> 3        30  0.0
#> 4       300  2.4
#> 5        30  0.0
#> 6       300  2.8
#> 7        30  0.0
#> 8       300  3.2
#> 9        30  0.0
#> 10      300  3.6
#> 11       30  0.0
#> 12      300  4.0
#> 13       30  0.0
#> 14      300  4.4
#> 15       30  0.0
#> 16      300  4.8
#> 17       30  0.0
#> 18      300  5.2
#> 19       10  0.0
```

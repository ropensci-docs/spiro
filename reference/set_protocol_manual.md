# Manually setting a testing profile

`set_protocol_manual()` allows to set any user-defined load profile for
an exercise test.

## Usage

``` r
set_protocol_manual(duration, load = NULL)

# Default S3 method
set_protocol_manual(duration, load)

# S3 method for class 'data.frame'
set_protocol_manual(duration, load = NULL)
```

## Arguments

- duration:

  Either a numeric vector containing the duration (in seconds) of each
  load step, or a `data.frame` containing columns for duration and load.

- load:

  A numeric vector of the same length as `duration` containing the
  corresponding load of each step. Not needed, if load and duration are
  both given in a `data.frame` as the first argument of the function.

## Value

A `data.frame` with the duration and load of each protocol step.

## Methods (by class)

- `set_protocol_manual(default)`: Default method when duration and load
  are given separately

- `set_protocol_manual(data.frame)`: Method for data frames with a
  duration and a load column

## See also

[set_protocol](https://docs.ropensci.org/spiro/reference/set_protocol.md)
for protocol setting with helper functions.

[get_protocol](https://docs.ropensci.org/spiro/reference/get_protocol.md)
For automated extracting of protocols from raw data.

## Examples

``` r
set_protocol_manual(
  duration = c(300, 120, 300, 60, 300),
  load = c(3, 5, 3, 6, 3)
)
#>   duration load
#> 1      300    3
#> 2      120    5
#> 3      300    3
#> 4       60    6
#> 5      300    3

# using a data.frame as input
pt_data <- data.frame(
  duration = c(180, 150, 120, 90, 60, 30),
  load = c(200, 250, 300, 350, 400, 450)
)
set_protocol_manual(pt_data)
#>   duration load
#> 1      180  200
#> 2      150  250
#> 3      120  300
#> 4       90  350
#> 5       60  400
#> 6       30  450
```

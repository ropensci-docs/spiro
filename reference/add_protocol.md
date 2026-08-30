# Add a test protocol to an exercise testing data set

`add_protocol()` adds a predefined test protocol to an existing set of
data from an exercise test.

## Usage

``` r
add_protocol(data, protocol)
```

## Arguments

- data:

  A spiro `data.frame` containing the exercise testing data.

- protocol:

  A `data.frame` containing the test protocol, as created by
  [`set_protocol`](https://docs.ropensci.org/spiro/reference/set_protocol.md),
  [`set_protocol_manual`](https://docs.ropensci.org/spiro/reference/set_protocol_manual.md)
  or
  [`get_protocol`](https://docs.ropensci.org/spiro/reference/get_protocol.md).

## Value

A `data.frame` of the class `spiro` with cardiopulmonary parameters and
the corresponding load data.

## See also

[set_protocol](https://docs.ropensci.org/spiro/reference/set_protocol.md)
for protocol setting with helper functions.

[set_protocol_manual](https://docs.ropensci.org/spiro/reference/set_protocol_manual.md)
for manual protocol design.

[get_protocol](https://docs.ropensci.org/spiro/reference/get_protocol.md)
For automated extraction of protocols from raw data.

## Examples

``` r
# Get example data
file <- spiro_example("zan_gxt")

s <- spiro(file)
out <- add_protocol(
  s,
  set_protocol(pt_pre(60), pt_steps(300, 50, 50, 7, 30))
)
head(out)
#>   load step time    VO2   VCO2    RR   VT    VE HR PetO2 PetCO2 VO2_rel
#> 1    0    0    1     NA     NA    NA   NA    NA NA    NA     NA      NA
#> 2    0    0    2     NA     NA    NA   NA    NA NA    NA     NA      NA
#> 3    0    0    3     NA     NA    NA   NA    NA NA    NA     NA      NA
#> 4    0    0    4 399.08 323.70 13.94 0.77 10.72 NA    NA     NA    6.05
#> 5    0    0    5 409.83 330.26 14.50 0.74 10.66 NA    NA     NA    6.21
#> 6    0    0    6 420.58 336.82 15.06 0.71 10.60 NA    NA     NA    6.37
#>   VCO2_rel RE  RER  CHO   FO
#> 1       NA NA   NA   NA   NA
#> 2       NA NA   NA   NA   NA
#> 3       NA NA   NA   NA   NA
#> 4      4.9 NA 0.81 0.20 0.13
#> 5      5.0 NA 0.81 0.19 0.13
#> 6      5.1 NA 0.80 0.19 0.14
```

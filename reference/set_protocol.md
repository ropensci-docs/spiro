# Setting an exercise testing profile

`set_protocol()` allows to set a load profile for an exercise test based
on profile sections.

## Usage

``` r
set_protocol(...)

pt_pre(duration)

pt_wu(duration, load, rest.duration = 0)

pt_steps(
  duration,
  load,
  increment,
  count,
  rest.duration = 0,
  last.duration = NULL
)

pt_const(duration, load, count, rest.duration = 0, last.duration = NULL)
```

## Arguments

- ...:

  Functions related to sections of the load profile, such as `pt_pre`,
  `pt_wu`, `pt_const` or `pt_step`. Sections will be evaluated in the
  order they are entered.

- duration:

  A number, giving the duration of the test section or a single load
  within the test section (in seconds).

- load:

  A number, giving the (initial) load of a section.

- rest.duration:

  A number, specifying the duration of (each) rest (in seconds).

- increment:

  A number, giving the difference in load between the current and the
  following load step.

- count:

  An integer for the number of load sections.

- last.duration:

  A number, giving the duration of the last load step (in seconds).

## Value

A `data.frame` with the duration and load of each protocol step.

## Functions

- `pt_pre()`: Add pre-measures to a load protocol

- `pt_wu()`: Add a warm up to a load protocol

- `pt_steps()`: Add a stepwise load protocol

- `pt_const()`: Add a constant load protocol

## See also

[set_protocol_manual](https://docs.ropensci.org/spiro/reference/set_protocol_manual.md)
for manual protocol design.

[get_protocol](https://docs.ropensci.org/spiro/reference/get_protocol.md)
for automated extracting of protocols from raw data.

## Examples

``` r
set_protocol(pt_pre(60), pt_wu(300, 100), pt_steps(180, 150, 25, 8, 30))
#>    duration load
#> 1        60    0
#> 2       300  100
#> 3       180  150
#> 4        30    0
#> 5       180  175
#> 6        30    0
#> 7       180  200
#> 8        30    0
#> 9       180  225
#> 10       30    0
#> 11      180  250
#> 12       30    0
#> 13      180  275
#> 14       30    0
#> 15      180  300
#> 16       30    0
#> 17      180  325
```

# Import and process raw data from metabolic carts/spiroergometric measures

`spiro()` wraps multiple functions to import and process raw data from
metabolic carts into a `data.frame`.

## Usage

``` r
spiro(
  file,
  device = NULL,
  bodymass = NULL,
  hr_file = NULL,
  hr_offset = 0,
  protocol = NULL,
  anonymize = TRUE
)
```

## Arguments

- file:

  The absolute or relative path of the file that contains the gas
  exchange data.

- device:

  A character string, specifying the device for measurement. By default
  the device type is guessed by the characteristics of the `file`. This
  can be overridden by setting the argument to `"cortex"`, `"cosmed"`,
  `"vyntus"` or `"zan"`.

- bodymass:

  Numeric value for the individual's body mass, if the default value
  saved in the `file` should be overridden.

- hr_file:

  The absolute or relative path of a `*tcx` file that contains
  additional heart rate data.

- hr_offset:

  An integer, corresponding to the temporal offset of the heart-rate
  file. By default the start of the heart rate measurement is linked to
  the start of the gas exchange measurement. A positive value means,
  that the heart rate measurement started after the begin of the gas
  exchange measurements; a negative value means it started before.

- protocol:

  A `data.frame` by
  [`set_protocol`](https://docs.ropensci.org/spiro/reference/set_protocol.md)
  or
  [`set_protocol_manual`](https://docs.ropensci.org/spiro/reference/set_protocol_manual.md)
  containing the test protocol. This is automatically guessed by
  default. Set to NA to skip protocol guessing.

- anonymize:

  Whether meta data should be anonymized during import. Defaults to
  TRUE. See
  [`get_anonid`](https://docs.ropensci.org/spiro/reference/get_anonid.md)
  for more information.

## Value

A `data.frame` of the class `spiro` with cardiopulmonary parameters
interpolated to seconds and the corresponding load data.

The attribute `"protocol"` provides additional information on the
underlying testing protocol. The attribute `"info"` contains additional
meta data from the original raw data file. The attribute `"raw"` gives
the imported raw data (without interpolation, similar to calling
[`spiro_raw`](https://docs.ropensci.org/spiro/reference/spiro_raw.md)).

## Details

This function performs multiple operations on raw data from metabolic
carts. It imports the raw data from a file, which might be complemented
by an additional `.tcx` file with heart rate data.

After using this function, you may summarize the resulting data frame
with
[`spiro_summary`](https://docs.ropensci.org/spiro/reference/spiro_summary.md)
and
[`spiro_max`](https://docs.ropensci.org/spiro/reference/spiro_max.md),
or plot it with
[`spiro_plot`](https://docs.ropensci.org/spiro/reference/spiro_plot.md).

## Import

Different metabolic carts yield different output formats for their data.
By default, this function will guess the used device based on the
characteristics of the given file. This behavior can be overridden by
explicitly stating the `device` argument.

The currently supported metabolic carts are:

- **CORTEX** (`.xlsx`, `.xls` or files `.xml` in English or German
  language)

- **COSMED** (`.xlsx` or `.xls` files, in English or German language)

- **Vyntus** (`.txt` files in English, French, German or Norwegian
  language)

- **ZAN** (`.dat` files in German language, usually with names in the
  form of `"EXEDxxx"`)

The spiro function can import personal meta data (name, sex, birthday,
...). By default this data is anonymized with `anonymize = TRUE`, see
[`get_anonid`](https://docs.ropensci.org/spiro/reference/get_anonid.md)
for more information.

## Processing

Breath-by-breath data is linearly interpolated to get data points for
every full second. Based on the given load data, the underlying exercise
protocol is guessed and applied to the data. If no load data is
available or the protocol guess turns wrong, you can manually specify
the exercise `protocol` by using
[`set_protocol`](https://docs.ropensci.org/spiro/reference/set_protocol.md)
or
[`set_protocol_manual`](https://docs.ropensci.org/spiro/reference/set_protocol_manual.md).
If you want to skip the automated protocol guessing without providing an
alternative, set `protocol = NA`. Note that in this case, some functions
relying on load data (such as
[`spiro_summary`](https://docs.ropensci.org/spiro/reference/spiro_summary.md))
will not work.

Additional variables of gas exchange are calculated for further
analysis. Per default the body mass saved in the file's metadata is used
for calculating relative measures. It is possible to specify `bodymass`
manually to the function, overriding that value.

Protocols, heart rate data and body mass information can also be given
in a piping coding style using the functions
[`add_protocol`](https://docs.ropensci.org/spiro/reference/add_protocol.md),
[`add_hr`](https://docs.ropensci.org/spiro/reference/add_hr.md) and
[`add_bodymass`](https://docs.ropensci.org/spiro/reference/add_bodymass.md)
(see examples).

## Examples

``` r
# get example file
file <- spiro_example("zan_gxt")

out <- spiro(file)
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

# import with user-defined test profile
p <- set_protocol(pt_pre(60), pt_steps(300, 2, 0.4, 9, 30))
out2 <- spiro(file, protocol = p)
head(out2)
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

# import with additional heart rate data
oxy_file <- spiro_example("zan_ramp")
hr_file <- spiro_example("hr_ramp.tcx")

out3 <- spiro(oxy_file, hr_file = hr_file)
head(out3)
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

# use the add_* functions in a pipe
# Note: base R pipe requires R version 4.1 or greater)
if (FALSE) { # \dontrun{
spiro(file) |>
  add_hr(hr_file = hr_file, hr_offset = 0) |>
  add_bodymass(68.2)
} # }
```

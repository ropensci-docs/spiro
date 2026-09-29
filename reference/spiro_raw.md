# Get raw data from a metabolic cart file or an imported spiro object

`spiro_raw()` retrieves cardiopulmonary raw data from various types of
metabolic cart files, or from objects previously imported and processed
with [`spiro`](https://docs.ropensci.org/spiro/reference/spiro.md).

## Usage

``` r
spiro_raw(data, device = NULL, anonymize = TRUE)

# Default S3 method
spiro_raw(data, device = NULL, anonymize = TRUE)

# S3 method for class 'spiro'
spiro_raw(data, device = NULL, anonymize = TRUE)
```

## Arguments

- data:

  Either the absolute or relative path of the file that contains the gas
  exchange data, or a data frame of the class `spiro`, usually the
  output of the
  [`spiro`](https://docs.ropensci.org/spiro/reference/spiro.md)
  function.

- device:

  A character string, specifying the device for measurement. By default
  the device type is guessed by the characteristics of the `file`. This
  can be overridden by setting the argument to `"cortex"`, `"cosmed"`,
  `"vyntus"` or `"zan"`.

- anonymize:

  Whether meta data should be anonymized during import. Defaults to
  TRUE. See
  [`get_anonid`](https://docs.ropensci.org/spiro/reference/get_anonid.md)
  for more information.

## Value

A `data.frame` with data. The attribute `info` contains addition
meta-data retrieved from the original file.

## Details

The default way of importing data into the spiro package is using the
[`spiro`](https://docs.ropensci.org/spiro/reference/spiro.md) function.
Besides importing this will perform further processing steps such as the
interpolation of data or the calculation of additional variables. But in
some cases the original raw data may be preferable compared to the
processed raw data. `spiro_raw` can either retrieve the raw data from an
already imported data set or from a new raw data file.

## Methods (by class)

- `spiro_raw(default)`: Method for direct import from metabolic cart raw
  data file

- `spiro_raw(spiro)`: Method for objects of class `spiro`, usually files
  previously imported and processed with
  [`spiro`](https://docs.ropensci.org/spiro/reference/spiro.md)

## Examples

``` r
# Get example data
file <- spiro_example("zan_gxt")

# direct import of raw data
out <- spiro_raw(file)
head(out)
#>    time VO2 VCO2    RR   VT    VE HR load PetO2 PetCO2
#> 1  3.44 393  320 13.62 0.79 10.76 NA    0    NA     NA
#> 2  7.25 434  345 15.76 0.67 10.51 NA    0    NA     NA
#> 3 10.73 440  352 17.14 0.76 12.96 NA    0    NA     NA
#> 4 13.97 582  451 18.63 0.65 12.13 NA    0    NA     NA
#> 5 17.20 837  677 18.47 1.07 19.71 NA    0    NA     NA
#> 6 20.39 902  753 18.87 1.19 22.42 NA    0    NA     NA

# retrieval of raw data from previously processed object
s <- spiro(file)
out2 <- spiro_raw(s)
head(out2)
#>    time VO2 VCO2    RR   VT    VE HR load PetO2 PetCO2
#> 1  3.44 393  320 13.62 0.79 10.76 NA    0    NA     NA
#> 2  7.25 434  345 15.76 0.67 10.51 NA    0    NA     NA
#> 3 10.73 440  352 17.14 0.76 12.96 NA    0    NA     NA
#> 4 13.97 582  451 18.63 0.65 12.13 NA    0    NA     NA
#> 5 17.20 837  677 18.47 1.07 19.71 NA    0    NA     NA
#> 6 20.39 902  753 18.87 1.19 22.42 NA    0    NA     NA
```

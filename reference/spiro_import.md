# Import raw data from spiroergometric devices (deprecated)

This function has been deprecated as of package version `0.2.0`. It will
be removed in the next version release. Please use
[`spiro`](https://docs.ropensci.org/spiro/reference/spiro.md) for
automated import and processing or
[`spiro_raw`](https://docs.ropensci.org/spiro/reference/spiro_raw.md) to
import only raw data.

## Usage

``` r
spiro_import(file, device = NULL, anonymize = TRUE)
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

- anonymize:

  Whether meta data should be anonymized during import. Defaults to
  TRUE. See
  [`get_anonid`](https://docs.ropensci.org/spiro/reference/get_anonid.md)
  for more information.

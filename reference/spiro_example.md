# Get path to spiro example

`spiro_example` returns the file path for example data files within the
`spiro` package.

## Usage

``` r
spiro_example(file = NULL)
```

## Arguments

- file:

  Name of the file, either "zan_gxt", "zan_ramp" or "hr_ramp.tcx". Leave
  the argument empty to get a vector with the paths of all three example
  files.

## Value

A character vector with the absolute file path of the example file(s).

## Examples

``` r
# get path of a specific example data file
spiro_example("zan_gxt")
#> [1] "/github/home/R/x86_64-pc-linux-gnu-library/4.6/spiro/extdata/zan_gxt"

# get all paths of example data files
spiro_example()
#> [1] "/github/home/R/x86_64-pc-linux-gnu-library/4.6/spiro/extdata/hr_ramp.tcx"
#> [2] "/github/home/R/x86_64-pc-linux-gnu-library/4.6/spiro/extdata/zan_gxt"    
#> [3] "/github/home/R/x86_64-pc-linux-gnu-library/4.6/spiro/extdata/zan_ramp"   
```

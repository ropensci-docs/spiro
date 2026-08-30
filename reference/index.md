# Package index

## General data import and processing

- [`spiro()`](https://docs.ropensci.org/spiro/reference/spiro.md) :
  Import and process raw data from metabolic carts/spiroergometric
  measures
- [`add_bodymass()`](https://docs.ropensci.org/spiro/reference/add_bodymass.md)
  : Calculate additional variables related to body mass for
  cardiopulmonary exercise testing data
- [`spiro_raw()`](https://docs.ropensci.org/spiro/reference/spiro_raw.md)
  : Get raw data from a metabolic cart file or an imported spiro object
- [`spiro_import()`](https://docs.ropensci.org/spiro/reference/spiro_import.md)
  : Import raw data from spiroergometric devices (deprecated)
- [`get_anonid()`](https://docs.ropensci.org/spiro/reference/get_anonid.md)
  : Get the anonymization id from personal data

## Working with additional heart rate data

- [`add_hr()`](https://docs.ropensci.org/spiro/reference/add_hr.md) :
  Import and add heart rate data to cardiopulmonary exercise testing
  data

## Data filtering

- [`spiro_smooth()`](https://docs.ropensci.org/spiro/reference/spiro_smooth.md)
  : Apply a smoothing filter to data from cardiopulmonary exercise
  testing.
- [`bw_filter()`](https://docs.ropensci.org/spiro/reference/bw_filter.md)
  : Smooth data with a (zero-phase) Butterworth filter

## Working with protocols

- [`add_protocol()`](https://docs.ropensci.org/spiro/reference/add_protocol.md)
  : Add a test protocol to an exercise testing data set
- [`get_protocol()`](https://docs.ropensci.org/spiro/reference/get_protocol.md)
  : Guess a test protocol from a corresponding exercise testing data set
- [`set_protocol_manual()`](https://docs.ropensci.org/spiro/reference/set_protocol_manual.md)
  : Manually setting a testing profile
- [`set_protocol()`](https://docs.ropensci.org/spiro/reference/set_protocol.md)
  [`pt_pre()`](https://docs.ropensci.org/spiro/reference/set_protocol.md)
  [`pt_wu()`](https://docs.ropensci.org/spiro/reference/set_protocol.md)
  [`pt_steps()`](https://docs.ropensci.org/spiro/reference/set_protocol.md)
  [`pt_const()`](https://docs.ropensci.org/spiro/reference/set_protocol.md)
  : Setting an exercise testing profile

## Summarizing

- [`spiro_summary()`](https://docs.ropensci.org/spiro/reference/spiro_summary.md)
  : Summarize data from cardiopulmonary exercise testing for each load
  step
- [`spiro_max()`](https://docs.ropensci.org/spiro/reference/spiro_max.md)
  : Return maximum values from cardiopulmonary exercise tests

## Plotting

- [`spiro_plot()`](https://docs.ropensci.org/spiro/reference/spiro_plot.md)
  : Plot data from cardiopulmonary exercise data files

## General package functions

- [`spiro-package`](https://docs.ropensci.org/spiro/reference/spiro-package.md)
  : spiro: Manage Data from Cardiopulmonary Exercise Testing
- [`spiro_example()`](https://docs.ropensci.org/spiro/reference/spiro_example.md)
  : Get path to spiro example
- [`knit_print(`*`<spiro>`*`)`](https://docs.ropensci.org/spiro/reference/knit_print.spiro.md)
  : Printing spiro data frames in a knitr context
- [`print(`*`<spiro>`*`)`](https://docs.ropensci.org/spiro/reference/print.spiro.md)
  : Printing spiro data frames

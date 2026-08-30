# Get the anonymization id from personal data

`get_anonid()` returns the anonymization id corresponding to given
personal data.

## Usage

``` r
get_anonid(name, surname, birthday = NULL)
```

## Arguments

- name:

  A character string, containing the participant's name as present in
  the raw data file.

- surname:

  A character string, containing the participant's surname as present in
  the raw data file.

- birthday:

  A character string, containing the participant's birthday as present
  in the raw data file. If no birthday data is available in the raw
  data, this is ignored.

## Value

A character string, containing the anonymized id.

## Details

By default, the spiro package anonymizes personal information obtained
from file meta data. The data are saved to the "info" attribute of a
spiro() call. The default anonymization ensures that no personal
information is accidentally revealed, e.g. by sharing spiro outputs as
.Rda files.

While there is no way to directly deanonymize the data, get_anonid()
allows you to recreate the ids, when meta data (name, surname and
birthday) are known. Birthday is only used within the id generation if
available in the original raw data.

To disable the anonymization process during import use
`spiro(anonymize = FALSE)`

## Examples

``` r
get_anonid("Jesse", "Owens", "12.09.1913")
#> [1] "e09d4015"
```

# pillar 1.1.0.9000 (2018-02-09)

- New styling helper `style_subtle_num()`.
- Very small numbers (like `1e-310`) are now printe corectly (tidyverse/tibble#377).
- Fix representation of right-hand side for `getOption(pillar.sigfig) >= 6` (tidyverse/tibble#380).
- The decimal dot is now always printed for numbers of type `numeric`. Trailing zeros are not displayed anymore if all displayed numbers are whole numbers.
- The new option `pillar.subtle_num` (default: `FALSE`) decides if numbers use subtle highlighting for digits that are considered insignificant.
- For decimal numbers, every third digit is underlined. This gives a better idea of the order of magnitude of the numbers. The first and last digit is never underlined.
- Decimal values longer than 13 characters always print in
  scientific notation.
- Fix computation of significant figures for numbers with absolute value >= 1 (#98).
- Logical columns are displayed as `TRUE` and `FALSE` again (#95).


# pillar 1.1.0 (2018-01-14)

- `NA` values are now shown in plain red, without changing the background color (#70).
- New options to control the output, with defaults that match the current behavior unless stated otherwise:
    - `pillar.sigfig` to control the number of significant digits, for highlighting and truncation (#72),
    - `pillar.subtle` to specify if insignificant digits should be printed in gray (#72),
    - `pillar.neg` to specify if negative digits should be printed in red,
    - `pillar.bold` to specify if column headers should be printed in bold (default: `FALSE`, #76),
    - `pillar.min_title_chars` to specify the minimum number of characters to display for each column name (default: 15 characters, #75).
- Shortened abbreviations for types: complex: cplx -> cpl, function: fun -> fn, factor: fctr -> fct (#71).
- Date columns now show sub-seconds if the `digits.secs` option is set (#74).
- Very wide tibbles now print faster (#85).


# pillar 1.0.1 (2017-11-27)

- Work around failing CRAN tests on Windows.


# pillar 1.0.0 (2017-11-16)

Initial release.

## User functions

    pillar(x, title = NULL, width = NULL, ...)
    colonnade(x, has_row_id = TRUE, width = NULL, ...)
    squeeze(x, width = NULL, ...)

## Functions for implementers of data types

    new_pillar_shaft_simple(formatted, ..., width = NULL, align = "left", min_width = NULL, na_indent = 0L)
    new_pillar_shaft(x, ..., width, min_width = width, subclass)
    new_ornament(x, width = NULL, align = NULL)
    get_extent(x)
    get_max_extent(x)

## Utilities

    dim_desc(x)
    style_na(x)
    style_neg(x)
    style_num(x, negative, significant = rep_along(x, TRUE))
    style_subtle(x)

## Testing helper

    expect_known_display(object, file, ..., width = 80L, crayon = TRUE)

## Own S3 methods

    pillar_shaft(x, ...) # AsIs, Date, POSIXt, character, default, list, logical, numeric
    type_sum(x) # AsIs, Date, POSIXct, data.frame, default, difftime, factor, ordered
    is_vector_s3(x) # Date, POSIXct, data.frame, default, difftime, factor, ordered
    obj_sum(x) # AsIs, POSIXlt, default, list
    extra_cols(x, ...) # squeezed_colonnade

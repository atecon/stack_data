# Stack Data Package Documentation

This package provides functions for "un-stacking" a panel dataset and stacking a time-series dataset.

For questions and bug reports, please use the gretl mailing list. Source code and test scripts can be found at URL: https://github.com/atecon/stack_data

# Overview

## unstack()

The `unstack()` function isolates the unit-specific time-series of a panel dataset with `k` units into separate columns of a matrix. This function has no built-in counterpart in gretl.

## stack_data()

The `stack_data()` function stacks a list of series vertically and stores the resulting series in a separate data file. This function can be applied within both loop-blocks and function-blocks, unlike Gretl's built-in `stack()` function which cannot change the dataset's dimension within a function-block.

## stack_matdata()

The `stack_matdata()` function stacks a list of series vertically and returns the stacked data as a matrix. This function operates in-memory, making it useful for large datasets.


# Public Functions

**stack_data(L, filename, series_name, series_description)**

Vertically stacks data from a list of series into a single series and stores the resulting series in a specified file. The returned matrix includes three series:

1. `unit_id`: A numeric identifier for each stacked series.
2. `obs_id`: A unit-specific running number from 1 to `T`.
3. The stacked series itself.

*Arguments:*

- `L`: List of series to stack.
- `filename`: Full path and filename where the dataset will be stored.
- `series_name` (optional): Name of the compiled series (default: `"stacked_series"`).
- `series_description` (optional): Descriptive label for the variable (default: `""`).

*Return:*

- Returns `0` if the stacked dataset is successfully stored; otherwise, returns `1`.

**stack_matdata(L, series_name[null])**

Works similarly to `stack_data()` but returns a matrix instead. The matrix comprises three columns:

1. `unit_id`: An index referring to each stacked series.
2. `obs_id`: A unit-specific running number from 1 to `T` (observations).
3. The stacked series itself.

*Arguments:*

- `L`: List of series to stack.
- `series_name` (optional): Name of the compiled series (default: `"stacked_series"`).

*Return:*

- Returns a non-empty matrix on success; otherwise, returns an empty matrix.

**unstack(x, series_name[null], names_array[null], fix_names[TRUE])**

Works only for panel data. For a panel with `k` units and `T` unit-specific observations, series `x` is reshaped into a `T` by `(1 + k)` matrix. The first column refers to the observational index, while the remaining columns refer to grouped values of `x`.

The columns of the resulting matrix may include labels if either:

- A string-valued series `series_names`, or
- A string array with `k` elements is provided.

If both `series_names` and `names_array` are provided and valid, `series_names` takes precedence.

*Arguments:*

- `x`: Series to unstack.
- `series_names` (optional): String-valued series of unit names.
- `names_array` (optional): Array of names for each panel unit.
- `fix_names` (optional): Convert raw group names to valid gretl identifiers (default: `TRUE`).

*Return:*

- Returns a matrix of dimension `T` by `(1 + k)`.


# Changelog

## v1.1, August 2024

- Switch help text to markdown format, and improve text.
- Require at least gretl 2020c for quiet default loops.
- Bugfix: Remove 'const' qualifier for series which are 'null' per default.

## v1.0, March 2021

- Added `unstack()` function as proposed by Riccardo "Jack" Lucchetti.
- Added `stack_matdata()` function.
- Functions are tested with unit-tests.
- Updated documentation.
- Requires gretl version 2020b.
- Internal refactorings.

## v0.9, April 2020

- Initial release.
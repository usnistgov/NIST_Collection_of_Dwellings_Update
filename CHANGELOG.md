# Changelog

All notable changes to this repository are recorded here. Dates are ISO 8601.

## [1.0.1] - 2026-11-10

Corrections to categorical mappings in seven scripts. Outputs from the code
paths listed below differ from version 1.0.0 and should be regenerated.

### Fixed

- `update_values_recs97.py` (AHS 2021 mode): homes with `YRBUILT == 1980`
  (built 1980 to 1989) were assigned to year-built group 2 (1940 to 1969).
  They are now assigned to group 3 (1970 to 1989), matching the RECS 2020 mode.
- `characteristic_distribution.py` (AHS 2021 mode): one story is subtracted
  from `STORIES` when a basement is under the whole house. A one-story home
  with a full basement was left with zero stories and no `#_of_floors` value,
  and was dropped from the grouped tables. The subtraction now stops at 1.
- `characteristic_distribution.py`, `manufacured_house_us_rep.py`,
  `recs20_sqft_weighted_average.py`, `update_values_recs97.py` (RECS 2020
  mode): records with `TYPEHUQ == 5` and `building_units == 1` carried a
  placeholder string in `#_of_units`. They are now assigned code "1", the
  smallest apartment stratum.
- `recs20_sqft_weighted_average.py` (RECS 2020 mode): the two larger apartment
  strata were selected with a string comparison on `#_of_units`, which also
  matched the placeholder. They are now selected by the explicit codes "2"
  through "5". The weighted averages for all four apartment strata change.
- `recs_characteristic_distribution_test(ahs).py` and
  `recs_characteristic_distribution_test(year).py` (RECS 2015 mode): attached
  and detached homes of every size were assigned floor-area code "1". Homes of
  1,500 to 2,490 ft^2 now receive code "2" and homes of 2,500 ft^2 or more
  receive code "3", matching `recs_characteristic_distribution.py`.
- `recs_characteristic_distribution.py` and both `_test` variants (AHS 2019
  mode): `BATHROOMS` code '07' had no mapping. It is now mapped to zero full
  bathrooms and one half bathroom, as in the AHS 2021 mode.

## [1.0.0] - 2024-09-04

Initial public release.

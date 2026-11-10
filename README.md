# A Collection of Dwellings to Represent the U.S. Housing Stock (2024 Update)

Python scripts for processing American Housing Survey (AHS) and Residential Energy Consumption Survey (RECS) data to characterize the U.S. residential dwelling stock.

## Overview

This repository contains analysis scripts developed in support of NIST TN 2329, "A Collection of Dwellings to Represent the U.S. Dwelling Stock: 2024 Update." The scripts process federal housing survey data (RECS 2020 and AHS 2021; three scripts also accept RECS 2015 and AHS 2019) to produce weighted distributions of dwelling characteristics used to select representative prototypes for building energy and indoor air quality modeling.

Key capabilities:

- Weighted characteristic distributions from RECS 2020 and AHS 2021 survey data
- Cross-survey comparison (AHS vs. RECS)
- Square-footage-weighted averages
- Dwelling type and characteristic visualizations (Bokeh, matplotlib)
- Manufactured housing and air leakage analysis
- Historical data processing (RECS 1997)

## Disclaimer

Certain commercial equipment, instruments, software, or materials are identified in this repository in order to specify the experimental and analytical procedures adequately. Such identification is not intended to imply recommendation or endorsement of any product or service by NIST, nor is it intended to imply that the materials or equipment identified are necessarily the best available for the purpose.

## Repository Structure

```
NIST_Collection_of_Dwellings_Update/
├── src/                          # Analysis and processing scripts
│   ├── ahs21_weighted_average.py         # Weighted averages for AHS 2021 data
│   ├── ahs_recs_data_comparison.py       # AHS and RECS cross-survey comparison
│   ├── characteristic_distribution.py    # Dwelling characteristic distributions
│   ├── collectionofdwelling_piechart.py  # Pie charts of dwelling type data
│   ├── manufacured_house_us_rep.py       # Manufactured housing analysis
│   ├── nist_housing_visualization.py     # Interactive housing data visualization
│   ├── nist_housing_viz_fixed.py         # Updated housing visualization
│   ├── recs20_sqft_weighted_average.py   # RECS 2020 square-footage weighted averages
│   ├── recs_characteristic_distribution.py          # RECS dwelling characteristic distributions
│   ├── recs_characteristic_distribution_test(ahs).py  # RECS vs. AHS validation
│   ├── recs_characteristic_distribution_test(year).py # Year-over-year comparison
│   ├── update_values_recs97.py           # 1997-style groupings applied to RECS 2020 or AHS 2021
│   ├── us_air_leakage_distribution.py    # U.S. air leakage distribution analysis
│   └── wap_calc.py                       # Weatherization Assistance Program calculations
│
├── data/                             # Survey data (not committed; layout under Data Sources)
│
├── results/                          # Analysis outputs (not committed)
│   ├── figures/                      # Generated plots
│   ├── tables/                       # Summary tables
│   └── output_data/                  # Processed output files
│
├── environment.yaml                  # Conda environment specification
├── data_config.json                  # Local data paths (gitignored)
├── data_config.template.json         # Template for data configuration
├── CHANGELOG.md                      # Version history
├── CITATION.cff                      # Citation metadata
├── CODEMETA.yaml                     # NIST Software Portal metadata
├── CODEOWNERS                        # Repository ownership
├── LICENSE.md                        # NIST software licensing statement
├── .gitignore
└── README.md
```

## Installation

### 1. Clone the Repository

```bash
git clone git@github.com:usnistgov/NIST_Collection_of_Dwellings_Update.git
cd NIST_Collection_of_Dwellings_Update
```

### 2. Create the Conda Environment

```bash
conda env create -f environment.yaml
conda activate cod
```

### 3. Configure Data Paths

```bash
cp data_config.template.json data_config.json
```

Edit `data_config.json` and set the paths for your machine:

```json
{
  "data_dir": "C:/Users/YourName/path/to/data",
  "results_dir": "C:/Users/YourName/path/to/results"
}
```

`data_config.json` is listed in `.gitignore` and should not be committed. Use `data_config.template.json` as a reference when setting up on a new machine.

## Data Sources

The scripts read survey files from the folder set as `data_dir` in `data_config.json`, using this layout:

```
<data_dir>/
├── recs_data/
│   ├── 2015/recs2015_public_v4.csv
│   └── 2020/
│       ├── recs2020_public_v1_data.csv
│       ├── recs2020_public_v2.csv
│       └── RECS2020_NIST.csv
└── ahs_data/
    ├── 2019/household.csv
    └── 2021/household.csv
```

- **RECS 2015 and RECS 2020 public microdata**: [EIA Residential Energy Consumption Survey](https://www.eia.gov/consumption/residential/)
- **AHS 2019 and AHS 2021 household files**: [U.S. Census American Housing Survey](https://www.census.gov/programs-surveys/ahs.html)
- **`RECS2020_NIST.csv`**: a RECS 2020 file prepared for NIST that is not public. It carries `building_units`, the number of units in the building, which the public microdata does not include. The RECS 2020 mode of `characteristic_distribution.py`, `manufacured_house_us_rep.py`, `recs20_sqft_weighted_average.py`, and `update_values_recs97.py` reads this file and cannot be run without it. The AHS 2021 mode of the same scripts uses the public `household.csv`.

`data_config.template.json` lists every file the scripts expect, including the 1997 files used for historical comparison.

## Usage

Activate the conda environment and run scripts from the repository root:

```bash
conda activate cod

# Dwelling characteristic distributions from RECS 2020 (needs RECS2020_NIST.csv)
python src/characteristic_distribution.py

# Square-footage-weighted averages (needs RECS2020_NIST.csv in RECS 2020 mode)
python src/recs20_sqft_weighted_average.py

# AHS vs. RECS comparison
python src/ahs_recs_data_comparison.py
```

## Version History

See [CHANGELOG.md](CHANGELOG.md). Version 1.0.1 corrects categorical mappings in seven scripts; outputs from the affected code paths differ from version 1.0.0.

## Citation

If you use this software in your research, please cite:

```bibtex
@software{lima2024dwellings,
  author    = {Lima, Nathan M.},
  title     = {A Collection of Dwellings to Represent the {U.S.} Housing Stock
               (2024 Update) Associated Python Scripts},
  year      = {2024},
  publisher = {National Institute of Standards and Technology},
  doi       = {10.18434/mds2-3488},
  url       = {https://github.com/usnistgov/NIST_Collection_of_Dwellings_Update}
}
```

**Related Publication:**

```bibtex
@techreport{lima2025collection,
  author      = {Lima, Nathan M. and Persily, Andrew K. and Emmerich, Steven J.},
  title       = {A Collection of Dwellings to Represent the {U.S.} Dwelling Stock:
                 2024 Update},
  institution = {National Institute of Standards and Technology},
  year        = {2025},
  type        = {NIST Technical Note},
  number      = {NIST TN 2329},
  address     = {Gaithersburg, MD},
  doi         = {10.6028/NIST.TN.2329},
  url         = {https://doi.org/10.6028/NIST.TN.2329}
}
```

## Contact

- **PI:** [Dr. Nathan Lima](https://www.nist.gov/people/dr-nathan-lima)
- **NIST Organizational Unit:** [Engineering Laboratory](https://www.nist.gov/el)
- **Division:** [Building Energy and Environment Division](https://www.nist.gov/el/beed)
- **Group:** [Indoor Air Quality and Ventilation Group](https://www.nist.gov/el/beed/indoor-air-quality-ventilation)
- **Email:** nathan.lima@nist.gov

## Acknowledgments

This research was conducted at the National Institute of Standards and Technology (NIST) as part of the [Indoor Air Quality and Ventilation Group](https://www.nist.gov/el/beed/indoor-air-quality-ventilation). Andrew K. Persily and Steven J. Emmerich served as project advisers.

## License

This software was developed by employees of the National Institute of Standards and Technology (NIST), an agency of the Federal Government, and is being made available as a public service. See [LICENSE.md](LICENSE.md) for the full NIST licensing statement.

---

For questions or issues, please open an issue on the GitHub repository or contact the project authors.

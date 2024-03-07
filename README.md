# xhydro-testdata

Testing data to support the xHydro and xDatasets projects.

## Contributing

In order to add a new dataset to the `xHydro`/`xDatasets` testing data, please ensure you perform the following:

1. Create a new branch: `git checkout -b my_new_testdata_branch`
2. Place your dataset within an appropriate subdirectory (or create a new one: `mkdir data`).
3. Run the md5 checksum generation script: `python report_check_sums.py`
4. Commit your changes: `git add * && git commit -m "added my_new_testdata"`
5. Open a Pull Request.

If you wish to perform preliminary tests against the dataset on a particular branch/commit, this can be done with the following procedure:

* To gather a single file:
```python
import pooch

GITHUB_URL = "https://github.com/hydrologie/xhydro-testdata"
BRANCH_OR_COMMIT_HASH = "my_development_branch"

test_data_path = pooch.retrieve(
    url=f"{GITHUB_URL}/raw/{BRANCH_OR_COMMIT_HASH}/data/my_test_data.nc",
    known_hash="md5:1234567890abcdef",
)

# If your testing data is `xarray`-readable, you can then use the following:
import xarray as xr

ds = xr.open_dataset(test_data_path)
```

## Loading data

If you wish to load data from this repository, this can be done with the following procedure:

* To gather a single file (using the `streamflow_BCC-CSM1.1-m_rcp45.nc` file as an example):
```python
import pooch
import xarray as xr

GITHUB_URL = "https://github.com/hydrologie/xhydro-testdata"
BRANCH_OR_COMMIT_HASH = "main"

test_data_path = pooch.retrieve(
    url=f"{GITHUB_URL}/raw/{BRANCH_OR_COMMIT_HASH}/data/cc_indicators/streamflow_BCC-CSM1.1-m_rcp45.nc",
    known_hash="md5:0ac83a4ee9dceecda68ac1ee542f50de",
)
ds = xr.open_dataset(test_data_path)
```

* To gather multiple files stored within a zip archive (using the `reference.zip` file as an example):
```python
from pathlib import Path
from zipfile import ZipFile

import pooch
import xarray as xr

GITHUB_URL = "https://github.com/hydrologie/xhydro-testdata"
BRANCH_OR_COMMIT_HASH = "main"

test_data_path = pooch.retrieve(
    url=f"{GITHUB_URL}/raw/{BRANCH_OR_COMMIT_HASH}/data/cc_indicators/reference.zip",
    known_hash="md5:192544f3a081375a81d423e08038d32a",
)

directory_to_extract_to = Path(test_data_path).parent  # Extract to the same directory as the zip file
with ZipFile(test_data_path, 'r') as zip_ref:
    zip_ref.extractall(directory_to_extract_to)
    files = zip_ref.namelist()
files = [directory_to_extract_to / f for f in files]

# Exactly how you open the files depends on the structure of the data. This will work for the reference.zip file:
ds = xr.open_mfdataset(files, combine="nested", concat_dim="platform")
```

[//]: # (Code below this line is autogenerated by `report_check_sums.py`)
## Available datasets

### Files

| File | Size | Checksum |
| ---- | ---- | -------- |
| data/cc_indicators/reference.zip | 23.7 kiB | 192544f3a081375a81d423e08038d32a |
| data/cc_indicators/streamflow_BCC-CSM1.1-m_rcp45.nc | 730.1 kiB | 0ac83a4ee9dceecda68ac1ee542f50de |
| data/cc_indicators/deltas.zip | 1.6 MiB | ce6371e073e5324f9ade385c1c03e7eb |
| data/LSTM_data/LSTM_test_data_local.nc | 118.0 kiB | 2abfe4dd0287a43c1ab40372f4fc4de8 |
| data/LSTM_data/LSTM_test_data.nc | 325.1 kiB | e7f1ddba0cf3dc3c5c6aa28a0c504fa2 |
| data/optimal_interpolation/OI_data.zip | 2.9 MiB | 1ab72270023366d0410eb6972d1e2656 |
| data/optimal_interpolation/OI_data_corrected.zip | 3.2 MiB | acdf90b78b53595eb97ff0e84fc07aa8 |

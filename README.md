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

* To open multiple files stored within a zip archive (using the `reference.zip` file as an example):
```python
import pooch
import xarray as xr

GITHUB_URL = "https://github.com/hydrologie/xhydro-testdata"
BRANCH_OR_COMMIT_HASH = "main"

files = pooch.retrieve(
    url=f"{GITHUB_URL}/raw/{BRANCH_OR_COMMIT_HASH}/data/cc_indicators/reference.zip",
    known_hash="md5:192544f3a081375a81d423e08038d32a",
    processor=pooch.Unzip()
)

# Exactly how you open the files depends on the structure of the data. This will work for the reference.zip file:
ds = xr.open_mfdataset(files, combine="nested", concat_dim="platform")
```

* You can also simply extract the files to a directory:
```python
from pathlib import Path
from zipfile import ZipFile

import pooch

GITHUB_URL = "https://github.com/hydrologie/xhydro-testdata"
BRANCH_OR_COMMIT_HASH = "main"

test_data_path = pooch.retrieve(
    url=f"{GITHUB_URL}/raw/{BRANCH_OR_COMMIT_HASH}/data/cc_indicators/reference.zip",
    known_hash="md5:192544f3a081375a81d423e08038d32a",
)

directory_to_extract_to = Path(test_data_path).parent  # To extract to the same directory as the zip file
with ZipFile(test_data_path, 'r') as zip_ref:
    zip_ref.extractall(directory_to_extract_to)
    files = zip_ref.namelist()
```

[//]: # (Code below this line is autogenerated by `report_check_sums.py`)
## Available datasets

### Files

| File | Size | Checksum |
| ---- | ---- | -------- |
| data/ravenpy/ERA5_Riviere_Rouge_global.nc | 150.7 kiB | de985fa27ddceac690aeb34182a93f11 |
| data/ravenpy/Debit_Riviere_Rouge.nc | 343.5 kiB | 5b0feedc34333244b1d9e9c251323478 |
| data/pmp/CMIP.CCCma.CanESM5.historical.r1i1p1f1.fx.gn.zarr/y/0 | 32.0 B | c1087eeb56ca7f31278ffe35865fc317 |
| data/pmp/CMIP.CCCma.CanESM5.historical.r1i1p1f1.fx.gn.zarr/x/0 | 32.0 B | e4153fe01e22a1f10f616905fcbbcc6d |
| data/pmp/CMIP.CCCma.CanESM5.historical.r1i1p1f1.fx.gn.zarr/orog/0.0 | 266.0 B | 73f3b39db9640e1a20447347f232dce8 |
| data/pmp/CMIP.CCCma.CanESM5.historical.r1i1p1f1.fx.gn.zarr/lon_bounds/0.0 | 172.0 B | 01bcaffcee72c69009599e203fe50bf8 |
| data/pmp/CMIP.CCCma.CanESM5.historical.r1i1p1f1.fx.gn.zarr/lat_bounds/0.0 | 204.0 B | d896da4a2ba534d1b4c2fd9dccce4504 |
| data/pmp/CMIP.CCCma.CanESM5.historical.r1i1p1f1.day.gn.zarr/zg/7.0.0.0 | 312.3 kiB | de0e3aee622dcb74699018f5d424194d |
| data/pmp/CMIP.CCCma.CanESM5.historical.r1i1p1f1.day.gn.zarr/zg/6.0.0.0 | 350.0 kiB | 0f46a36fec219dbdf1a66a21b16b2365 |
| data/pmp/CMIP.CCCma.CanESM5.historical.r1i1p1f1.day.gn.zarr/zg/5.0.0.0 | 349.8 kiB | c3bb4533ed7c97a43ba808d9ea0e441a |
| data/pmp/CMIP.CCCma.CanESM5.historical.r1i1p1f1.day.gn.zarr/zg/4.0.0.0 | 350.3 kiB | 98731e0dbecd48599dfed9a6657d61e2 |
| data/pmp/CMIP.CCCma.CanESM5.historical.r1i1p1f1.day.gn.zarr/zg/3.0.0.0 | 349.9 kiB | e7853259bed9e4ca75baa2918b99ae54 |
| data/pmp/CMIP.CCCma.CanESM5.historical.r1i1p1f1.day.gn.zarr/zg/2.0.0.0 | 349.9 kiB | 63f69a3777728ac93f8bacdb797c121c |
| data/pmp/CMIP.CCCma.CanESM5.historical.r1i1p1f1.day.gn.zarr/zg/1.0.0.0 | 350.3 kiB | a074378098d6f4d5b578c4c68446ecf2 |
| data/pmp/CMIP.CCCma.CanESM5.historical.r1i1p1f1.day.gn.zarr/zg/0.0.0.0 | 349.7 kiB | c559a6c4f6339319c6052adf3a87aa16 |
| data/pmp/CMIP.CCCma.CanESM5.historical.r1i1p1f1.day.gn.zarr/y/0 | 32.0 B | c1087eeb56ca7f31278ffe35865fc317 |
| data/pmp/CMIP.CCCma.CanESM5.historical.r1i1p1f1.day.gn.zarr/x/0 | 32.0 B | e4153fe01e22a1f10f616905fcbbcc6d |
| data/pmp/CMIP.CCCma.CanESM5.historical.r1i1p1f1.day.gn.zarr/time_bounds/0.0 | 791.0 B | 959720facdfea909d20d2b5cede347dd |
| data/pmp/CMIP.CCCma.CanESM5.historical.r1i1p1f1.day.gn.zarr/time/0 | 1.3 kiB | c2cf87d551029f023567f0251d74e238 |
| data/pmp/CMIP.CCCma.CanESM5.historical.r1i1p1f1.day.gn.zarr/tas/0.0.0 | 336.3 kiB | 022fbdbb5ad73f763fd143babc3da1f1 |
| data/pmp/CMIP.CCCma.CanESM5.historical.r1i1p1f1.day.gn.zarr/snw/0.0.0 | 1.2 MiB | 721f0642c3e31617a07fff9f72689cdc |
| data/pmp/CMIP.CCCma.CanESM5.historical.r1i1p1f1.day.gn.zarr/rf/0.0.0 | 40.5 kiB | 2ce15504c37f721df530ac435b94d4a7 |
| data/pmp/CMIP.CCCma.CanESM5.historical.r1i1p1f1.day.gn.zarr/prsn/0.0.0 | 26.7 kiB | 1707b5ed961b3a081c0da7e95a5a155b |
| data/pmp/CMIP.CCCma.CanESM5.historical.r1i1p1f1.day.gn.zarr/pr/0.0.0 | 39.7 kiB | 7c485bec5fe7eedc20a626b27572ae41 |
| data/pmp/CMIP.CCCma.CanESM5.historical.r1i1p1f1.day.gn.zarr/plev/0 | 80.0 B | dc999432541da64ed5dae4580f6ae156 |
| data/pmp/CMIP.CCCma.CanESM5.historical.r1i1p1f1.day.gn.zarr/lon_bounds/0.0 | 48.0 B | 550658b148dceb16410652c38cd91c57 |
| data/pmp/CMIP.CCCma.CanESM5.historical.r1i1p1f1.day.gn.zarr/lat_bounds/0.0 | 48.0 B | d07d4b23d16b8c9d6783348f5b4b4d1d |
| data/pmp/CMIP.CCCma.CanESM5.historical.r1i1p1f1.day.gn.zarr/hus/8.0.0.0 | 270.3 kiB | 3303a15a8825f0c76b93bdea44c2f78c |
| data/pmp/CMIP.CCCma.CanESM5.historical.r1i1p1f1.day.gn.zarr/hus/7.0.0.0 | 314.1 kiB | 5e69a05a9a0390887339fa8af65e1b97 |
| data/pmp/CMIP.CCCma.CanESM5.historical.r1i1p1f1.day.gn.zarr/hus/6.0.0.0 | 313.9 kiB | 192206eef8f9e01720a076287fc37766 |
| data/pmp/CMIP.CCCma.CanESM5.historical.r1i1p1f1.day.gn.zarr/hus/5.0.0.0 | 313.8 kiB | 930694d14aca4535a199f4a53f7ce70f |
| data/pmp/CMIP.CCCma.CanESM5.historical.r1i1p1f1.day.gn.zarr/hus/4.0.0.0 | 314.1 kiB | 0cb78b539ec9ffafae0cd0d99ac0a97b |
| data/pmp/CMIP.CCCma.CanESM5.historical.r1i1p1f1.day.gn.zarr/hus/3.0.0.0 | 313.7 kiB | 1d4034c1b331d47bd2dc1aa9616abc19 |
| data/pmp/CMIP.CCCma.CanESM5.historical.r1i1p1f1.day.gn.zarr/hus/2.0.0.0 | 314.0 kiB | 9f3fda18604a8441a370dde8b81651bc |
| data/pmp/CMIP.CCCma.CanESM5.historical.r1i1p1f1.day.gn.zarr/hus/1.0.0.0 | 313.9 kiB | 5fabbde713f1ca4434ab3ee63354591d |
| data/pmp/CMIP.CCCma.CanESM5.historical.r1i1p1f1.day.gn.zarr/hus/0.0.0.0 | 313.8 kiB | 3959dd8047c5d118f2db68e3cd4b9b46 |
| data/pmp/CMIP.CCCma.CanESM5.historical.r1i1p1f1.day.gn.zarr/height/0 | 8.0 B | c96d5502b9fd39f24913025b5127ccc1 |
| data/optimal_interpolation/OI_data_corrected.zip | 3.2 MiB | acdf90b78b53595eb97ff0e84fc07aa8 |
| data/optimal_interpolation/OI_data.zip | 2.9 MiB | 1ab72270023366d0410eb6972d1e2656 |
| data/LSTM_data/single_watershed.nc | 1.2 MiB | b1dfe4641321f63fb9198e9538fd679b |
| data/LSTM_data/multiple_watersheds.nc | 3.2 MiB | 31e1ae3ffcfd14d6a92faefd3d8bd57a |
| data/LSTM_data/LSTM_test_data_local.nc | 118.0 kiB | 2abfe4dd0287a43c1ab40372f4fc4de8 |
| data/LSTM_data/LSTM_test_data.nc | 325.1 kiB | e7f1ddba0cf3dc3c5c6aa28a0c504fa2 |
| data/extreme_value_analysis/genpareto.zip | 136.0 kiB | ecb74164db4bbfeabfc5e340b11e7ae8 |
| data/extreme_value_analysis/genextreme.zip | 228.0 kiB | cc2ff7c93949673a6acf00c7c2fac20b |
| data/cc_indicators/streamflow_BCC-CSM1.1-m_rcp45.nc | 730.1 kiB | 0ac83a4ee9dceecda68ac1ee542f50de |
| data/cc_indicators/reference.zip | 23.7 kiB | 192544f3a081375a81d423e08038d32a |
| data/cc_indicators/deltas.zip | 1.6 MiB | ce6371e073e5324f9ade385c1c03e7eb |

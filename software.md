# Software

## IMAP Data Access Software

Users may programmatically access IMAP data through the IMAP Data Access API, which provides both a command-line utility
and Python library for accessing the data.  See the
[supporting documentation](https://github.com/IMAP-Science-Operations-Center/imap-data-access/blob/main/README.md) for
further details.

A simple example of how to query and download data is provided below:

### Installation and Help

```bash
pip install imap-data-access
imap-data-access -h
```

### Command Line Utility

#### Base Command Arguments

```bash
imap-data-access query # or
imap-data-access download # or
```

Add the '-h' help flag with any base command for more information

#### Query / Search for data

Example: Find all files from the SWE instrument

```bash
$ imap-data-access query --instrument swe
Found [3] matching files
|-----------------------------------------------------------------------------------------------------------------------------------|
| Instrument | Data Level | Descriptor      | Start Date | Repointing | Version | Filename                                          |
|-----------------------------------------------------------------------------------------------------------------------------------|
| swe        | l0         | raw             | 20240510   |            | v022    | imap_swe_l0_raw_20240510_v022.pkts                |
| swe        | l1a        | sci             | 20240510   |            | v022    | imap_swe_l1a_sci_20240510_v022.cdf                |
| swe        | l1b        | sci             | 20240510   |            | v022    | imap_swe_l1b_sci_20240510_v022.cdf                |
|-----------------------------------------------------------------------------------------------------------------------------------|
```

Example: Find all files during the year 2024 and return the response as raw json

```bash
$ imap-data-access query --start-date 20240101 --end-date 20241231 --output-format json
[{'file_path': 'imap/swe/l0/2024/01/imap_swe_l0_sci_20240105_v001.pkts', 'instrument': 'swe', 'data_level': 'l0', 'descriptor': 'sci', 'start_date': '20240105', 'version': 'v001', 'extension': 'pkts'},
 {'file_path': 'imap/swe/l0/2024/01/imap_swe_l0_sci_20240105_v001.pkts', 'instrument': 'swe', 'data_level': 'l0', 'descriptor': 'sci', 'start_date': '20240105', 'version': 'v001', 'extension': 'pkts'}]
```

#### Download a file

Example: Download a level 0 SWE file on 2024/01/05

```bash
$ imap-data-access download imap/swe/l0/2024/01/imap_swe_l0_sci_20240105_v001.pkts
Successfully downloaded the file to: <IMAP_DATA_DIR>/imap/swe/l0/2024/01/imap_swe_l0_sci_20240105_v001.pkts
```

### Python Package

```python
import imap_data_access

# Search for files
results = imap_data_access.query(instrument="mag", data_level="l0")
# results is a list of dictionaries
# [{'file_path': 'imap/swe/l0/2024/01/imap_swe_l0_sci_20240105_v001.pkts', 'instrument': 'swe', 'data_level': 'l0', 'descriptor': 'sci', 'start_date': '20240105','version': 'v001', 'extension': 'pkts'},
#  {'file_path': 'imap/swe/l0/2024/01/imap_swe_l0_sci_20240105_v001.pkts', 'instrument': 'swe', 'data_level': 'l0', 'descriptor': 'sci', 'start_date': '20240105', 'version': 'v001', 'extension': 'pkts'}]

# Download a file that was returned from the search
imap_data_access.download("imap/mag/l0/2024/01/imap_mag_l0_raw_202040101_v001.pkts")
```


## Open Source Software

All software written for the IMAP Science Data Center is open-source and publicly available from the
[`IMAP-Science-Operations-Center` GitHub organization](https://github.com/IMAP-Science-Operations-Center).

This includes software within the following repositories:

| Name | Description | 
|---|---| 
| [imap_processing](https://github.com/IMAP-Science-Operations-Center/imap_processing) | Software for performing L0->L2 data processing | 
| [imap_L3_processing](https://github.com/IMAP-Science-Operations-Center/imap_L3_processing) | Software for performing L3 data processing |
| [sds-data-manager](https://github.com/IMAP-Science-Operations-Center/sds-data-manager) | Software for building and configuring AWS architecture to support data processing | 
| [imap-data-access](https://github.com/IMAP-Science-Operations-Center/imap-data-access) | Package and command line utility for users to download, query, and upload data from the IMAP Science Data Center | 
| [imap-sdc-website](https://github.com/IMAP-Science-Operations-Center/imap-sdc-website) | Materials for the IMAP SDC website | 
| [ialirt-data-access](https://github.com/IMAP-Science-Operations-Center/ialirt-data-access) | Package and command line utility for users to download and query data from I-ALiRT | 
| [SAMMI](https://github.com/swxsoc/sammi/) | Contains tools for managing CDF metadata, created as a collaboration between SWxSOC and IMAP SDC |

Software releases are available on PyPI for [`imap_processing`](https://pypi.org/project/imap-processing/) and
[`imap-data-access`](https://pypi.org/project/imap-data-access/).  DOIs for `imap_processing` are available on
[Zenodo](https://zenodo.org/records/14782117).
# SDMX to V4 tool

For creating SDMX to V4 pipelines for CMD.


# Install

`pip install git+https://github.com/ONS-OpenData/SDMXtoV4.git`


# Usage

This section is concerned with use inside a python script. Some command line usage guidence is provided at the end.


## Main Extracton Functions

```python
from SDMXtoV4.SDMXtoV4 import SDMXtoV4, SDMXsummary

# ALWAYS use this first. An example of the summary output is included below.
# will tell you if obs, time and geography dimensions have been automatically found.
SDMXsummary(<v4file>)

# main function - to output a converted csv.
# [dimensions] is just a list of dimensions as listed by SDMXsummary.
SDMXTOV4(<v4file>, [dimensions])

# you can use keywords: obs=, time=, and geo= to specify these dimension where needed.
SDMXTOV4(<v4file>, [dimensions], obs="obsDimensionName")

# you can also return the contents of the CSV directly as a pandas dataframe instead of writing.
dataFrame = SDMXTOV4(<v4file>, [dimensions], returnFrame=True)

```

Example SDMXsummary output
```
------------------
Mandatory Dimensions
----------------
These will be included automatically in the V4 transformation.

Time Column:       time_period
Geography Column:  ref_area
Observations:      obs_value


Optional Dimensions
-----------------------
OCCURANCES  | ITEM
-----------------------
1           | accounting_entry
89          | activity
1           | adjustment
1           | compiling_org
1           | conf_status
1           | counterpart_area
1           | counterpart_sector
1           | decimals
1           | embargo_date
1           | expenditure
1           | freq
14          | instr_asset
1           | obs_status
3           | prices
1           | ref_sector
2           | ref_year_price
5           | sto
1           | table_identifier
1           | title
1           | transformation
1           | unit_measure
1           | unit_mult

```

## Other Functions
```python
from SDMXtoV4.SDMXtoV4 import SDMXflattenWithCodes, SDMXflattenWithoutCodes

# Flatten all dimensions into a simple one-row-per-obs
# Convert all the codelists and codes using sdmx.org APIs
SDMXflattenWithCodes(<v4file>)

# Flatten all dimensions into a simple one-row-per-obs
SDMXflattenWithoutCodes(<v4file>)

```


# On the command line


v4 transformation

NOTE = the string commands at the end (after "SDMX>") must start with "dimension=" and must only contain spaces between keywords.

```python SDMXtoV4.py -v4 <SOURCE SDMX> dimension=this,that,other obs=obColName```


SDMX summary

```python SMXtoV4.py -list <SOURCE SDMX>```


Flatten without code transformation

```python SMXtoV4.py -raw <SOURCE SDMX>```


Flatten with code transformation

```python SMXtoV4.py -tran <SOURCE SDMX>```


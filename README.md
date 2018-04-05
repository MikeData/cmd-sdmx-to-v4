# SDMX to V4 tool

Intended to allow us to quickly create simple SDMX to V4 pipelines for CMD.


# Install

`pip install git+https://github.com/ONS-OpenData/SDMXtoV4.git`


# Usage

This section is concerned without use inside a python script. Some command line usage guidence is provided at the end.


## Main Extracton Functions

```python
from SDMXtoV4.SDMXtoV4 import SDMXtoV4, SDMXsummary, SDMXflattenWithCodes, SDMXflattenWithoutCodes

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

```

## Other Functions
```
from SDMXtoV4.SDMXtoV4 import SDMXflattenWithCodes, SDMXflattenWithoutCodes

# Flatten all dimensions into a simple one-row-per-obs
# Convert all the codelists and codes using sdmx.org APIs
SDMXflattenWithCodes(<v4file>)

# Flatten all dimensions into a simple one-row-per-obs
SDMXflattenWithoutCodes(<v4file>)

```


# On the command line

v4 transformation
NOTE = the string commands at the end (after "SDMX>") must start with dimensions and must only contain spaces between keywords.
```python SDMXtoV4.py -v4 <SOURCE SDMX> dimension=this,that,other obs=obColName

SDMX summary
```python SMXtoV4.py -list <SOURCE SDMX>```

Flatten without code transformation
```python SMXtoV4.py -raw <SOURCE SDMX>```

Flatten with code transformation
```python SMXtoV4.py -tran <SOURCE SDMX>```


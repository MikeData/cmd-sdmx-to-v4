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
SDMXsummary(<v4file>)

# main function - to output a converted csv
# [dimensions] is just a list of dimensions as listed by SDMXsummary
SDMXTOV4(<v4file>, [dimensions])

# you can always use the keywords obs=, time=, and geo= to specify where those mandatory dimension are not found.
SDMXTOV4(<v4file>, [dimensions], obs="obsDimensionName")

# you can also return the contents of the CSV directly as a pandas dataframe instead of writing
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


# Other Functionality

The rest of the functionality is based around helping you explore the data and getting you to the point where you can run a transform like the above example.

```python SMXtoV4.py -raw <SOURCE SDMX>```


Writes the whole SDMX file to simple flat file CSV.

```python SMXtoV4.py -tran <SOURCE SDMX>```


Writes the whole SDMX file to simple flat file CSV and uses codelists hosted on sdmx.org to translate the codes into labels.

```python SMXtoV4.py -list <SOURCE SDMX>```

Prints to screen a summary of the dimensions inside the SDMX dataset. This inludes whether or not the observations, time and geography dimensions have been automatically identified (if not - see below) as well as a list of all optional dimensions along with a count of the number of unique items in each.



# Obs, Time and Geography

The aim is for these to be automatially detected by the tool (you can check by using the -list switch).

If for any reason they arent you can pass this information in the the options string (the bit that contains "dimensions=X,Y").

Example:

```python SDMXtoV4.py -v4 <SOURCE SDMX> "time=my_time_column obs=obs_column dimensions=Industry,Age geo=area_dimension"```

The order does not matter but they must be delimited by spaces and no other spaces should be included in the string.



# Use as a Module

To run as part of a python script.

```
import SDMXtoV4 from SDMXtoV4

# To build a standard V4
SDMXtoV4(file, [dimensions])
```

If the script cannot automatically identify observations, time or geography (it'll tell you) you can pass in the relevent columns as optional keyword arguments.

```
SDMXTOV4(file, [dimensions], obs="ons_column")
```
The helper function can be called from within a script as follows:

```
from SDMXtoV4 import BUILDraw, BUILDtran, PRINTlist

BUILDraw(file)
BUILDtran(file)
PRINTlist(file)

```



# find-out-cases-and-total-deaths-occured-by-corona-in-india
Setup and usage
Install from pip with

pip install covid19dh
Importing the main function covid19()

from covid19dh import covid19
x, src = covid19() 
Package is regularly updated. Update with

pip install --upgrade covid19dh
Return values
The function covid19() returns 2 pandas dataframes:

the data and
references to the data sources.
Parametrization
Country
List of country names (case-insensitive) or ISO codes (alpha-2, alpha-3 or numeric). The list of ISO codes can be found here.

Fetching data from a particular country:

x, src = covid19("USA") # Unites States
Specify multiple countries at the same time:

x, src = covid19(["ESP","PT","andorra",250])
If country is omitted, the whole dataset is returned:

x, src = covid19()
Raw data
Logical. Skip data cleaning? Default True. If raw=False, the raw data are cleaned by filling missing dates with NaN values. This ensures that all locations share the same grid of dates and no single day is skipped. Then, NaN values are replaced with the previous non-NaN value or 0.

x, src = covid19(raw = False)
Date filter
Date can be specified with datetime.datetime, datetime.date or as a str in format YYYY-mm-dd.

from datetime import datetime
x, src = covid19("SWE", start = datetime(2020,4,1), end = "2020-05-01")
Level
Integer. Granularity level of the data:

Country level
State, region or canton level
City or municipality level
from datetime import date
x, src = covid19("USA", level = 2, start = date(2020,5,1))
Cache
Logical. Memory caching? Significantly improves performance on successive calls. By default, using the cached data is enabled.

Caching can be disabled (e.g. for long running programs) by:

x, src = covid19("FRA", cache = False)
Vintage
Logical. Retrieve the snapshot of the dataset that was generated at the end date instead of using the latest version. Default False.

To fetch e.g. US data that were accessible on 22th April 2020 type

x, src = covid19("USA", end = "2020-04-22", vintage = True)
The vintage data are collected at the end of the day, but published with approximately 48 hour delay, once the day is completed in all the timezones.

Hence if vintage = True, but end is not set, warning is raised and None is returned.

x, src = covid19("USA", vintage = True) # too early to get today's vintage
UserWarning: vintage data not available yet
Data Sources
The data sources are returned as second value.

from covid19dh import covid19
x, src = covid19("USA")
print(src)
Additional information
Find out more at https://covid19datahub.io


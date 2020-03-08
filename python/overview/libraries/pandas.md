---
description: >-
  Parse Excel and CSVs files quickly and easily with the pandas library for
  Python.
---

# Pandas

## Overview

 **pandas** is a [Python](https://www.python.org) package providing fast, flexible, and expressive data structures designed to make working with “relational” or “labeled” data both easy and intuitive. It aims to be the fundamental high-level building block for doing practical, **real world** data analysis in Python. Additionally, it has the broader goal of becoming **the most powerful and flexible open source data analysis / manipulation tool available in any language**. It is already well on its way toward this goal. \([source](https://pandas.pydata.org/pandas-docs/stable/getting_started/overview.html)\)

## Installing Pandas

Using Anaconda

```
$ conda install pandas
```

Using PyPI:

```bash
$ pip install pandas
```

{% hint style="info" %}
Full details found here: [https://pandas.pydata.org/pandas-docs/stable/getting\_started/install.html](https://pandas.pydata.org/pandas-docs/stable/getting_started/install.html)
{% endhint %}

## Reading Data

Pandas comes with functionality to read data from many file types including:

* CSV
* Excel
* HTML \(tables\)
* SQL
* BiqQuery
* etc

For most file-based reading, Pandas will accept as the first argument a local file \(e.g. `pd.read_csv('data.csv')` \), or a web URL \(e.g. `pd.read_csv('https://domain.com/data.csv')` \).

### CSV

For CSVs, Pandas handles the datatype setting for you. The most common named parameter sent with the `read_csv` method is `skiprows=1` when the inputted CSV has non-heading rows prior to the first row.

{% hint style="info" %}
Pandas API Reference for read\_csv function: [https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read\_csv.html](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_csv.html)
{% endhint %}

```bash
import pandas as pd
df = pd.read_csv('https://raw.githubusercontent.com/fivethirtyeight/data/master/airline-safety/airline-safety.csv')
df.head()
```

|  | airline | avail\_seat\_km\_per\_week | incidents\_85\_99 | fatal\_accidents\_85\_99 | fatalities\_85\_99 | incidents\_00\_14 | fatal\_accidents\_00\_14 | fatalities\_00\_14 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | Aer Lingus | 320906734 | 2 | 0 | 0 | 0 | 0 | 0 |
| 1 | Aeroflot\* | 1197672318 | 76 | 14 | 128 | 6 | 1 | 88 |
| 2 | Aerolineas Argentinas | 385803648 | 6 | 0 | 0 | 1 | 0 | 0 |
| 3 | Aeromexico\* | 596871813 | 3 | 1 | 64 | 5 | 0 | 0 |
| 4 | Air Canada | 1865253802 | 2 | 0 | 0 | 2 | 0 | 0 |

### Excel

For me, I use the `read_excel` method much less frequently than `read_csv` mostly due to habit and the assumption that the data is cleaner with a CSV.  Common named parameters would be `sheet_name = "Sheet1"` or `skip_rows=[1]`.

{% hint style="info" %}
Pandas API Reference for read\_excel function: [https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read\_excel.html](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_excel.html)
{% endhint %}

```bash
import pandas as pd
df = pd.read_excel('https://www2.census.gov/programs-surveys/popest/tables/2010-2019/state/totals/nst-est2019-01.xlsx', skiprows=3)
df.head()
```

|  | Unnamed: 0 | Census | Estimates Base | 2010 | 2011 | 2012 | 2013 | 2014 | 2015 | 2016 | 2017 | 2018 | 2019 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | United States | 308745538.0 | 308758105.0 | 309321666.0 | 311556874.0 | 313830990.0 | 315993715.0 | 318301008.0 | 320635163.0 | 322941311.0 | 324985539.0 | 326687501.0 | 328239523.0 |
| 1 | Northeast | 55317240.0 | 55318443.0 | 55380134.0 | 55604223.0 | 55775216.0 | 55901806.0 | 56006011.0 | 56034684.0 | 56042330.0 | 56059240.0 | 56046620.0 | 55982803.0 |
| 2 | Midwest | 66927001.0 | 66929725.0 | 66974416.0 | 67157800.0 | 67336743.0 | 67560379.0 | 67745167.0 | 67860583.0 | 67987540.0 | 68126781.0 | 68236628.0 | 68329004.0 |
| 3 | South | 114555744.0 | 114563030.0 | 114866680.0 | 116006522.0 | 117241208.0 | 118364400.0 | 119624037.0 | 120997341.0 | 122351760.0 | 123542189.0 | 124569433.0 | 125580448.0 |
| 4 | West | 71945553.0 | 71946907.0 | 72100436.0 | 72788329.0 | 73477823.0 | 74167130.0 | 74925793.0 | 75742555.0 | 76559681.0 | 77257329.0 | 77834820.0 | 78347268.0 |

### HTML Tables

This is a very handy function, where there is a table on a web page that you want to grab the data from. 

{% hint style="info" %}
Pandas API Reference for read\_html function: [https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read\_html.html](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_html.html)
{% endhint %}

```bash
import pandas as pd
df = pd.read_html('https://countrycode.org/', attrs = {'class': 'main-table'})
df[0].head()
```

|  | COUNTRY | COUNTRY CODE | ISO CODES | POPULATION | AREA KM2 | GDP $USD |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | Afghanistan | 93 | AF / AFG | 29121286 | 647500 | 20.65 Billion |
| 1 | Albania | 355 | AL / ALB | 2986952 | 28748 | 12.8 Billion |
| 2 | Algeria | 213 | DZ / DZA | 34586184 | 2381740 | 215.7 Billion |
| 3 | American Samoa | 1-684 | AS / ASM | 57881 | 199 | 462.2 Million |
| 4 | Andorra | 376 | AD / AND | 84000 | 468 | 4.8 Billion |




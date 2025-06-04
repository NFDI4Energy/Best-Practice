<!-- BEGIN-ANNOTATION: oeo -->
# The Dataset
The Marktstammdatenregister is a dataset of the German energy system provided by Bundesnetagentur under the open License `Datenlizenz Deutschland – Namensnennung – Version 2.0`. It contains almost every PV system, wind turbine, battery storage, hydropower plant, etc. in Germany. The dataset provides precise location information for every unit with an installed power larger than 30kW.


In this tutorial, we will work with the Marktstammdatenregister dataset. You will learn how to:

1. **Download today's version of the dataset**: We will use the Python package `open-mastr` to download the latest version of the Marktstammdatenregister dataset.

2. **Read the table of all wind turbines into a pandas dataframe**: Using `pandas`, we will read the data about wind turbines from the downloaded dataset and store it in a dataframe.

3. **Find installed capacity per German state**.

To complete this tutorial, you should have:

* Python installed
* Basic knowledge of Python programming and the `pandas` library
* Approximately 10 GB of free disk space available to store the downloaded dataset


# Let's start
1. Install open-mastr
<!-- END-ANNOTATION: oeo -->

```bash
pip install open-mastr 
```
<!-- BEGIN-ANNOTATION: oeo -->

2. Download the registry and parse the data on wind turbines
<!-- END-ANNOTATION: oeo -->
```python
from open_mastr import Mastr
db = Mastr()
db.download(data="wind")
```
<!-- BEGIN-ANNOTATION: oeo -->
Alternatively, other technologies like solar, storages, hydro etc can also be parsed. Find a full list at the [documentation page of open-mastr](https://open-mastr.readthedocs.io/en/latest/reference/basic/#open_mastr.Mastr.download)

3. Use pandas to read the wind turbine table to a dataframe
<!-- END-ANNOTATION: oeo -->
```python
import pandas as pd
table="wind_extended"
df = pd.read_sql(sql=table, con=db.engine)
```
<!-- BEGIN-ANNOTATION: oeo -->

4. As a final step, we want to see how much wind capacity is installed per german state. Hence we aggregate the installed power per state:
<!-- END-ANNOTATION: oeo -->
```python
grouped = (
    df.groupby("Bundesland")
    .agg(
        {"Nettonennleistung": lambda x: (x.sum() / 1e6)}
    )  # Divide by 1e6 to convert kW to GW
    .rename(columns={"Nettonennleistung": "total installed capacity [GW]"})
    .sort_values(by="total installed capacity [GW]", ascending=False)
)
print(grouped)
```
<!-- BEGIN-ANNOTATION: oeo -->
We see that in spring 2025, the state "Niedersachsen" had the highest installed capacity with almost 19GW.
<!-- END-ANNOTATION: oeo -->
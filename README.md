# cmput-191-assignment-3

## Analysis of the cost of 1kg of White Rice

### Source Data

First, I need to get the data for the price of a kg of white rice. I use [Numeo](https://www.numbeo.com/cost-of-living/prices_by_country.jsp?displayCurrency=CAD&itemId=115). I scrape the table on the website.

#### Clean the data

The source data table comes with a `rank` row, which is filled with `nan`. I remove it. I test for duplicate values by `.group()`ing on "Country", and test for non float values in the price column. I scatterplot the data to see if i makes sense and if there are any outliers. ![](initial_scatterplot.png)

# Tax rate data

Next, I need data for the sale tax in different countries. I get this data from [OECD](https://www.oecd.org/tax/tax-policy/tax-database/). The file is not a csv, it is an xlsl, so different code is needed to import it. 
```python
raw_tax_table = Table.from_df(pd.read_excel(url))
```
The table contains a lot of extra data:

![](mess_table.png)

It has data for many years, and extra information about each country. I `select` only the rows for country and 2021 tax rate, and filter for nan values to remove the extra information rows. I also remove the asterisks after the names of some countries, and convert the ercentage into a value that can be directly multiplied with price to get the total price with tax. ![](clean_tax_table.png)

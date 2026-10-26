---
title: Pandas DataFrames
teaching: 15
exercises: 15
---

::::::::::::::::::::::::::::::::::::::: objectives

- Select individual values from a Pandas dataframe.
- Select entire rows or entire columns from a dataframe.
- Select a subset of both rows and columns from a dataframe in a single operation.
- Select a subset of a DataFrame using conditional expressions.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- How can I do statistical analysis of tabular data?

::::::::::::::::::::::::::::::::::::::::::::::::::

## DataFrame Structure

A [DataFrame][pandas-dataframe] is a collection of [Series][pandas-series];
The DataFrame is the way Pandas represents a table, and Series is the data-structure
Pandas uses to represent a column.

Let's look at a larger dataset: `gapminder_gdp_asia.csv`. We're going to read it into a DataFrame called `gdp_asia` and specify `country` as the `index_col`.

```python
gdp_asia = pd.read_csv("data/gapminder_gdp_asia.csv", index_col="country")
```

We can use the `.head()` method to take a peek at the first n rows of a DataFrame.

```python
gdp_asia.head(5) # Look at the first five rowss
```

## Selecting a Column (Series) from a DataFrame
A **[Series](https://pandas.pydata.org/docs/reference/api/pandas.Series.html)** is a one-dimensional array with an index that corresponds to the indices of the parent DataFrame.

The fastest way to look at a single column in a DataFrame is to use `[]` and pass in the name of a column. Column names are strings, so you'll need to wrap the column name in quotes.

We can get a list of those columns using the `.columns` attribute.

```python
gdp_asia.columns
```
```output
Index(['gdpPercap_1952', 'gdpPercap_1957', 'gdpPercap_1962', 'gdpPercap_1967',
       'gdpPercap_1972', 'gdpPercap_1977', 'gdpPercap_1982', 'gdpPercap_1987',
       'gdpPercap_1992', 'gdpPercap_1997', 'gdpPercap_2002', 'gdpPercap_2007'],
      dtype='str')
```

Let's pick a column from the list above to select: 'gdpPercap_1987`.

```python
gdp_asia["gdpPercap_1987"] 
```
```output
country
Afghanistan             852.395945
Bahrain               18524.024060
Bangladesh              751.979403
Cambodia                683.895573
China                  1378.904018
Hong Kong China       20038.472690
India                   976.512676
Indonesia              1748.356961
Iran                   6642.881371
Iraq                  11643.572680
Israel                17122.479860
Japan                 22375.941890
Jordan                 4448.679912
Korea Dem. Rep.        4106.492315
Korea Rep.             8533.088805
Kuwait                28118.429980
Lebanon                5377.091329
Malaysia               5249.802653
Mongolia               2338.008304
Myanmar                 385.000000
Nepal                   775.632450
Oman                  18115.223130
Pakistan               1704.686583
Philippines            2189.634995
Saudi Arabia          21198.261360
Singapore             18861.530810
Sri Lanka              1876.766827
Syria                  3116.774285
Taiwan                11054.561750
Thailand               2982.653773
Vietnam                 820.799445
West Bank and Gaza     5107.197384
Yemen Rep.             1971.741538
Name: gdpPercap_1987, dtype: float64
```

Let's check the type of our selection.
```python
type(gdp_asia["gdpPercap_1987"]) # This is a Series
```
```output
pandas.Series
```
Keep in mind that like slicing from a string, selection from a DataFrame doesn't change the original DataFrame. 

## Aggregating with Series
Here are some common methods for *aggregation* that can be performed on quantitative Series.

```python
gdp_asia["gdpPercap_1987"].median()
```
```output
np.float64(4106.492315)
```

```python
gdp_asia["gdpPercap_1987"].max()
```
```output
np.float64(28118.42998)
```

```python
gdp_asia["gdpPercap_1987"].sum()
```
```output
np.float64(251071.4747551)s
```

## Plotting with `.hist()`
Another fun method for manipulating Series is the [**hist()**](https://pandas.pydata.org/docs/reference/api/pandas.Series.hist.html) method which shows the distribution of quantitative values within a Series. 

A histogram is a visualization that plots the bucketed values of a numeric variable against the frequency of that bucket.

```python
gdp_asia["gdpPercap_1987"].hist() # Default # of bins
```

Use the `bins=` parameter to adjust how many bins are in your histogram.

```python
gdp_asia["gdpPercap_2007"].hist(bins=5) # Fewer bins
```

## DataFrame Operations
We can use some of the same operations we used on Series on DataFrames, but they will return a **vectorized** result for each column rather than for the entire frame.

That is, they return a [min, max, etc.](https://pandas.pydata.org/docs/getting_started/intro_tutorials/06_calculate_statistics.html) for each column rather than one value for the entire frame.

```python
gdp_asia.max() 
```
```output
gdpPercap_1952    108382.35290
gdpPercap_1957    113523.13290
gdpPercap_1962     95458.11176
gdpPercap_1967     80894.88326
gdpPercap_1972    109347.86700
gdpPercap_1977     59265.47714
gdpPercap_1982     33693.17525
gdpPercap_1987     28118.42998
gdpPercap_1992     34932.91959
gdpPercap_1997     40300.61996
gdpPercap_2002     36023.10540
gdpPercap_2007     47306.98978
dtype: float64
```

```python
gdp_asia.median()
```
```output
gdpPercap_1952    1206.947913
gdpPercap_1957    1547.944844
gdpPercap_1962    1649.552153
gdpPercap_1967    2029.228142
gdpPercap_1972    2571.423014
gdpPercap_1977    3195.484582
gdpPercap_1982    4106.525293
gdpPercap_1987    4106.492315
gdpPercap_1992    3726.063507
gdpPercap_1997    3645.379572
gdpPercap_2002    4090.925331
gdpPercap_2007    4471.061906
dtype: float64
```



## Use `DataFrame.iloc[..., ...]` to select values by their (entry) position

To access a value at the position `[i,j]` of a DataFrame, where i and j are integers, we can use **iloc**. DataFrames provides an index as a way to identify the rows of the table; a row, then, has a position inside the table as well as a label, which uniquely identifies its entry in the DataFrame.

```python
gdp_asia.head(5)
```
```output
 	gdpPercap_1952 	gdpPercap_1957 	gdpPercap_1962 	gdpPercap_1967 	gdpPercap_1972 	gdpPercap_1977 	gdpPercap_1982 	gdpPercap_1987 	gdpPercap_1992 	gdpPercap_1997 	gdpPercap_2002 	gdpPercap_2007
country 												
Afghanistan 	779.445314 	820.853030 	853.100710 	836.197138 	739.981106 	786.113360 	978.011439 	852.395945 	649.341395 	635.341351 	726.734055 	974.580338
Bahrain 	9867.084765 	11635.799450 	12753.275140 	14804.672700 	18268.658390 	19340.101960 	19211.147310 	18524.024060 	19035.579170 	20292.016790 	23403.559270 	29796.048340
Bangladesh 	684.244172 	661.637458 	686.341554 	721.186086 	630.233627 	659.877232 	676.981866 	751.979403 	837.810164 	972.770035 	1136.390430 	1391.253792
Cambodia 	368.469286 	434.038336 	496.913648 	523.432314 	421.624026 	524.972183 	624.475478 	683.895573 	682.303175 	734.285170 	896.226015 	1713.778686
China    400.448611 	575.987001 	487.674018 	612.705693 	676.900092 	741.237470 	962.421381 	1378.904018 	1655.784158 	2289.234136 	3119.280896 	4959.114854
```

The `.iloc` or "integer position based indexing" ,ethod is designed to behave like the indexing you've already used for strings and lists.

To get a value at row i, column j use the following syntax for iloc. Remember, rows and columns are numbered starting at 0, just like in a string.

```python
gdp_asia.iloc[0, 1] # Row, column form
```
```output
np.float64(820.8530296)
```

This gives us the GDP of Afghanistan in 1957 because `Afghanistan` is the first row and the `gdpPercap_1957` column is the second column.

Just like with strings, we can pass in ranges indicated by `a:b` syntax to slice a range of columns or rows. Remember, ranges are inclusive at integer a of a:b but exclusive at integer b.

```python
gdp_asia.iloc[0:3, 1] # Second column of the first three rows
```
```output
country
Afghanistan      820.853030
Bahrain        11635.799450
Bangladesh       661.637458
Name: gdpPercap_1957, dtype: float64
```

You can slice by rows and columns at the same time.

```python
gdp_asia.iloc[0:3, 1:5] # This returns columns at indices 1-4 for first 3 rows
```
```output
gdpPercap_1957 	gdpPercap_1962 	gdpPercap_1967 	gdpPercap_1972
country 				
Afghanistan 	820.853030 	853.100710 	836.197138 	739.981106
Bahrain 	11635.799450 	12753.275140 	14804.672700 	18268.658390
Bangladesh 	661.637458 	686.341554 	721.186086 	630.233627
```

If you pass in a single number to `.iloc[]` rather than a range, Pandas will assume you want to see the row at that index.

```python
gdp_asia.iloc[0] # Returns the first row
```
```output
gdpPercap_1952    779.445314
gdpPercap_1957    820.853030
gdpPercap_1962    853.100710
gdpPercap_1967    836.197138
gdpPercap_1972    739.981106
gdpPercap_1977    786.113360
gdpPercap_1982    978.011439
gdpPercap_1987    852.395945
gdpPercap_1992    649.341395
gdpPercap_1997    635.341351
gdpPercap_2002    726.734055
gdpPercap_2007    974.580338
Name: Afghanistan, dtype: float64
```

## Use `DataFrame.loc[..., ...]` to select values by their names.

We can also use `.loc[i, j]` to [select values in a DataFrame by their label](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.loc.html#pandas.DataFrame.loc). Row indices can be numeric (default) or categorical (strings). Columns are almost always indexed by strings. Indexing with `.loc[i, j]` is also in row, column order.

The following use of `.loc[]` selects the value from column "gdpPercap_2002" from the row named "China". 
```python
gdp_asia.loc["China", "gdpPercap_2002"]
```
```output
np.float64(3119.280896)
```

## Use `:` on its own to mean all columns or all rows.

To refer to all rows or all columns when slicing, use the `:` symbol.

```python
gdp_asia.loc["Singapore", :]
```

```output
gdpPercap_1952     2315.138227
gdpPercap_1957     2843.104409
gdpPercap_1962     3674.735572
gdpPercap_1967     4977.418540
gdpPercap_1972     8597.756202
gdpPercap_1977    11210.089480
gdpPercap_1982    15169.161120
gdpPercap_1987    18861.530810
gdpPercap_1992    24769.891200
gdpPercap_1997    33519.476600
gdpPercap_2002    36023.105400
gdpPercap_2007    47143.179640
Name: Singapore, dtype: float64
```

```python
gdp_asia.loc[:, "gdpPercap_1952"]
```
```output
country
Afghanistan              779.445314
Bahrain                 9867.084765
Bangladesh               684.244172
Cambodia                 368.469286
China                    400.448611
Hong Kong China         3054.421209
India                    546.565749
Indonesia                749.681655
Iran                    3035.326002
Iraq                    4129.766056
Israel                  4086.522128
Japan                   3216.956347
Jordan                  1546.907807
Korea Dem. Rep.         1088.277758
Korea Rep.              1030.592226
Kuwait                108382.352900
Lebanon                 4834.804067
Malaysia                1831.132894
Mongolia                 786.566857
Myanmar                  331.000000
Nepal                    545.865723
Oman                    1828.230307
Pakistan                 684.597144
Philippines             1272.880995
Saudi Arabia            6459.554823
Singapore               2315.138227
Sri Lanka               1083.532030
Syria                   1643.485354
Taiwan                  1206.947913
Thailand                 757.797418
Vietnam                  605.066492
West Bank and Gaza      1515.592329
Yemen Rep.               781.717576
Name: gdpPercap_1952, dtype: float64
```

## Select multiple columns or rows using `DataFrame.loc` and a named slice.
We can also use `.loc[]` to return a range of consecutive columns or rows. However, slicing with **.loc[]** is **inclusive at both ends**. This is extremely confusing and is only done because it is designed to mimic R.

```python
gdp_asia.loc["Pakistan":"Singapore", "gdpPercap_1957":"gdpPercap_1972"]
```
```output
 	gdpPercap_1957 	gdpPercap_1962 	gdpPercap_1967 	gdpPercap_1972
country 				
Pakistan 	747.083529 	803.342742 	942.408259 	1049.938981
Philippines 	1547.944844 	1649.552153 	1814.127430 	1989.374070
Saudi Arabia 	8157.591248 	11626.419750 	16903.048860 	24837.428650
Singapore 	2843.104409 	3674.735572 	4977.418540 	8597.756202
```

## Result of slicing can be used in further operations.

- Usually don't just print a slice.
- All the statistical operators that work on entire dataframes
  work the same way on slices.
- E.g., calculate max of a slice.

```python
print(gdp_asia.loc["Pakistan":"Singapore", "gdpPercap_1957":"gdpPercap_1972"].max())
```

```output
gdpPercap_1957     8157.591248
gdpPercap_1962    11626.419750
gdpPercap_1967    16903.048860
gdpPercap_1972    24837.428650
dtype: float64
```

## Use comparisons to select data based on value.

- Comparison is applied element by element.
- Returns a similarly-shaped dataframe of `True` and `False`.

```python
# Use a subset of data to keep output readable.
europe = pd.read_csv("data/gapminder_gdp_europe.csv", index_col="country")
subset = europe.loc['Italy':'Poland', 'gdpPercap_1962':'gdpPercap_1972']
print('Subset of europe:\n', subset)
# Which values were greater than 10000 ?
print('\nWhere are values greater than 10000?', subset > 10000)
```
```output
Subset of europe:
             gdpPercap_1962  gdpPercap_1967  gdpPercap_1972
country
Italy           8243.582340    10022.401310    12269.273780
Montenegro      4649.593785     5907.850937     7778.414017
Netherlands    12790.849560    15363.251360    18794.745670
Norway         13450.401510    16361.876470    18965.055510
Poland          5338.752143     6557.152776     8006.506993

Where are values greater than 10000?
            gdpPercap_1962 gdpPercap_1967 gdpPercap_1972
country
Italy                False           True           True
Montenegro           False          False          False
Netherlands           True           True           True
Norway                True           True           True
Poland               False          False          False
```

## Select values or NaN using a Boolean mask.

- A frame full of Booleans is sometimes called a *mask* because of how it can be used.

```python
mask = subset > 10000
print(subset[mask])
```

```output
             gdpPercap_1962  gdpPercap_1967  gdpPercap_1972
country
Italy                   NaN     10022.40131     12269.27378
Montenegro              NaN             NaN             NaN
Netherlands     12790.84956     15363.25136     18794.74567
Norway          13450.40151     16361.87647     18965.05551
Poland                  NaN             NaN             NaN
```

- Get the value where the mask is true, and NaN (Not a Number) where it is false.
- Useful because NaNs are ignored by operations like max, min, average, etc.

```python
print(subset[subset > 10000].describe())
```

```output
       gdpPercap_1962  gdpPercap_1967  gdpPercap_1972
count        2.000000        3.000000        3.000000
mean     13120.625535    13915.843047    16676.358320
std        466.373656     3408.589070     3817.597015
min      12790.849560    10022.401310    12269.273780
25%      12955.737547    12692.826335    15532.009725
50%      13120.625535    15363.251360    18794.745670
75%      13285.513523    15862.563915    18879.900590
max      13450.401510    16361.876470    18965.055510
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Selection of Individual Values

Assume Pandas has been imported into your notebook
and the Gapminder GDP data for Europe has been loaded:

```python
import pandas as pd
europe = pd.read_csv('data/gapminder_gdp_europe.csv', index_col='country')
```

Write an expression to find the Per Capita GDP of Serbia in 2007.

:::::::::::::::  solution

## Solution

The selection can be done by using the labels for both the row ("Serbia") and the column ("gdpPercap\_2007"):

```python
print(europe.loc['Serbia', 'gdpPercap_2007'])
```

The output is

```output
9786.534714
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Extent of Slicing

1. Do the two statements below produce the same output?
2. Based on this,
  what rule governs what is included (or not) in numerical slices and named slices in Pandas?

```python
print(europe.iloc[0:2, 0:2])
print(europe.loc['Albania':'Belgium', 'gdpPercap_1952':'gdpPercap_1962'])
```

:::::::::::::::  solution

## Solution

No, they do not produce the same output! The output of the first statement is:

```output
        gdpPercap_1952  gdpPercap_1957
country                                
Albania     1601.056136     1942.284244
Austria     6137.076492     8842.598030
```

The second statement gives:

```output
        gdpPercap_1952  gdpPercap_1957  gdpPercap_1962
country                                                
Albania     1601.056136     1942.284244     2312.888958
Austria     6137.076492     8842.598030    10750.721110
Belgium     8343.105127     9714.960623    10991.206760
```

Clearly, the second statement produces an additional column and an additional row compared to the first statement.  
What conclusion can we draw? We see that a numerical slice, 0:2, *omits* the final index (i.e. index 2)
in the range provided,
while a named slice, 'gdpPercap\_1952':'gdpPercap\_1962', *includes* the final element.


:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Selecting Indices

Explain in simple terms what `idxmin` and `idxmax` do in the short program below.
When would you use these methods?

```python
europe = pd.read_csv('data/gapminder_gdp_europe.csv', index_col='country')
print(europe.idxmin())
print(europe.idxmax())
```

:::::::::::::::  solution

## Solution

For each column in `europe`, `idxmin` will return the index value corresponding to each column's minimum;
`idxmax` will do accordingly the same for each column's maximum value.

You can use these functions whenever you want to get the row index of the minimum/maximum value and not the actual minimum/maximum value.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Practice with Selection

Assume Pandas has been imported and the Gapminder GDP data for Europe has been loaded.
Write an expression to select each of the following:

1. GDP per capita for all countries in 1982.
2. GDP per capita for Denmark for all years.
3. GDP per capita for all countries for years *after* 1985.
4. GDP per capita for each country in 2007 as a multiple of
  GDP per capita for that country in 1952.

:::::::::::::::  solution

## Solution

1:

```python
europe['gdpPercap_1982']
```

2:

```python
europe.loc['Denmark',:]
```

3:

```python
europe.loc[:,'gdpPercap_1985':]
```

Pandas is smart enough to recognize the number at the end of the column label and does not give you an error, although no column named `gdpPercap_1985` actually exists. This is useful if new columns are added to the CSV file later.

4:

```python
europe['gdpPercap_2007']/europe['gdpPercap_1952']
```

:::::::::::::::::::::::::


::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Many Ways of Access

There are at least two ways of accessing a value or slice of a DataFrame: by name or index.
However, there are many others. For example, a single column or row can be accessed either as a `DataFrame`
or a `Series` object.

Suggest different ways of doing the following operations on a DataFrame:

1. Access a single column
2. Access a single row
3. Access an individual DataFrame element
4. Access several columns
5. Access several rows
6. Access a subset of specific rows and columns
7. Access a subset of row and column ranges

:::::::::::::::  solution

## Solution

1\. Access a single column:

```python
# by name
data["col_name"]   # as a Series
data[["col_name"]] # as a DataFrame

# by name using .loc
data.T.loc["col_name"]  # as a Series
data.T.loc[["col_name"]].T  # as a DataFrame

# Dot notation (Series)
data.col_name

# by index (iloc)
data.iloc[:, col_index]   # as a Series
data.iloc[:, [col_index]] # as a DataFrame

# using a mask
data.T[data.T.index == "col_name"].T
```

2\. Access a single row:

```python
# by name using .loc
data.loc["row_name"] # as a Series
data.loc[["row_name"]] # as a DataFrame

# by name
data.T["row_name"] # as a Series
data.T[["row_name"]].T # as a DataFrame

# by index
data.iloc[row_index]   # as a Series
data.iloc[[row_index]]   # as a DataFrame

# using mask
data[data.index == "row_name"]
```

3\. Access an individual DataFrame element:

```python
# by column/row names
data["column_name"]["row_name"]         # as a Series

data[["col_name"]].loc["row_name"]  # as a Series
data[["col_name"]].loc[["row_name"]]  # as a DataFrame

data.loc["row_name"]["col_name"]  # as a value
data.loc[["row_name"]]["col_name"]  # as a Series
data.loc[["row_name"]][["col_name"]]  # as a DataFrame

data.loc["row_name", "col_name"]  # as a value
data.loc[["row_name"], "col_name"]  # as a Series. Preserves index. Column name is moved to `.name`.
data.loc["row_name", ["col_name"]]  # as a Series. Index is moved to `.name.` Sets index to column name.
data.loc[["row_name"], ["col_name"]]  # as a DataFrame (preserves original index and column name)

# by column/row names: Dot notation
data.col_name.row_name

# by column/row indices
data.iloc[row_index, col_index] # as a value
data.iloc[[row_index], col_index] # as a Series. Preserves index. Column name is moved to `.name`
data.iloc[row_index, [col_index]] # as a Series. Index is moved to `.name.` Sets index to column name.
data.iloc[[row_index], [col_index]] # as a DataFrame (preserves original index and column name)

# column name + row index
data["col_name"][row_index]
data.col_name[row_index]
data["col_name"].iloc[row_index]

# column index + row name
data.iloc[:, [col_index]].loc["row_name"]  # as a Series
data.iloc[:, [col_index]].loc[["row_name"]]  # as a DataFrame

# using masks
data[data.index == "row_name"].T[data.T.index == "col_name"].T
```

4\. Access several columns:

```python
# by name
data[["col1", "col2", "col3"]]
data.loc[:, ["col1", "col2", "col3"]]

# by index
data.iloc[:, [col1_index, col2_index, col3_index]]
```

5\. Access several rows

```python
# by name
data.loc[["row1", "row2", "row3"]]

# by index
data.iloc[[row1_index, row2_index, row3_index]]
```

6\. Access a subset of specific rows and columns

```python
# by names
data.loc[["row1", "row2", "row3"], ["col1", "col2", "col3"]]

# by indices
data.iloc[[row1_index, row2_index, row3_index], [col1_index, col2_index, col3_index]]

# column names + row indices
data[["col1", "col2", "col3"]].iloc[[row1_index, row2_index, row3_index]]

# column indices + row names
data.iloc[:, [col1_index, col2_index, col3_index]].loc[["row1", "row2", "row3"]]
```

7\. Access a subset of row and column ranges

```python
# by name
data.loc["row1":"row2", "col1":"col2"]

# by index
data.iloc[row1_index:row2_index, col1_index:col2_index]

# column names + row indices
data.loc[:, "col1_name":"col2_name"].iloc[row1_index:row2_index]

# column indices + row names
data.iloc[:, col1_index:col2_index].loc["row1":"row2"]
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::


[pandas-dataframe]: https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html
[pandas-series]: https://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.html
[numpy]: https://www.numpy.org/


:::::::::::::::::::::::::::::::::::::::: keypoints

- Use `DataFrame.iloc[..., ...]` to select values by integer location.
- Use `:` on its own to mean all columns or all rows.
- Select multiple columns or rows using `DataFrame.loc` and a named slice.
- Result of slicing can be used in further operations.
- Use comparisons to select data based on value.
- Select values from a DataFrame using a Boolean mask.

::::::::::::::::::::::::::::::::::::::::::::::::::



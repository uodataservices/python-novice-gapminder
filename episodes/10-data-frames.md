---
title: Pandas DataFrames
teaching: 15
exercises: 15
---

::::::::::::::::::::::::::::::::::::::: objectives

- Select individual values from a Pandas dataframe.
- Select entire rows or entire columns from a dataframe.
- Select a subset of both rows and columns from a dataframe in a single operation.
- Construct simple Boolean expressions with comparisons.
- Select a subset of a dataframe by a single Boolean criterion.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- How can I do statistical analysis of tabular data?
- What are Booleans? How can I use them?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Note about Pandas DataFrames/Series

A [DataFrame][pandas-dataframe] is a collection of [Series][pandas-series];
The DataFrame is the way Pandas represents a table, and Series is the data-structure
Pandas use to represent a column.

Pandas is built on top of the [Numpy][numpy] library, which in practice means that
most of the methods defined for Numpy Arrays apply to Pandas Series/DataFrames.

What makes Pandas so attractive is the powerful interface to access individual records
of the table, proper handling of missing values, and relational-databases operations
between DataFrames.

## Selecting values

To access a value at the position `[i,j]` of a DataFrame, we have two options, depending on
what is the meaning of `i` in use.
Remember that a DataFrame provides an *index* as a way to identify the rows of the table;
a row, then, has a *position* inside the table as well as a *label*, which
uniquely identifies its *entry* in the DataFrame.

## Use `DataFrame.iloc[..., ...]` to select values by their (entry) position

- Can specify location by numerical index analogously to 2D version of character selection in strings.

```python
import pandas as pd
europe = pd.read_csv('data/gapminder_gdp_europe.csv', index_col='country')
print(europe.iloc[0, 0])
```

```output
1601.056136
```

## Use `DataFrame.loc[..., ...]` to select values by their (entry) label.

- Can specify location by row and/or column name.

```python
print(europe.loc["Albania", "gdpPercap_1952"])
```

```output
1601.056136
```

## Use `:` on its own to mean all columns or all rows.

- Just like Python's usual slicing notation.

```python
print(europe.loc["Albania", :])
```

```output
gdpPercap_1952    1601.056136
gdpPercap_1957    1942.284244
gdpPercap_1962    2312.888958
gdpPercap_1967    2760.196931
gdpPercap_1972    3313.422188
gdpPercap_1977    3533.003910
gdpPercap_1982    3630.880722
gdpPercap_1987    3738.932735
gdpPercap_1992    2497.437901
gdpPercap_1997    3193.054604
gdpPercap_2002    4604.211737
gdpPercap_2007    5937.029526
Name: Albania, dtype: float64
```

- Would get the same result printing `europe.loc["Albania"]` (without a second index).

```python
print(europe.loc[:, "gdpPercap_1952"])
```

```output
country
Albania                    1601.056136
Austria                    6137.076492
Belgium                    8343.105127
⋮ ⋮ ⋮
Switzerland               14734.232750
Turkey                     1969.100980
United Kingdom             9979.508487
Name: gdpPercap_1952, dtype: float64
```

- Would get the same result printing `europe["gdpPercap_1952"]`
- Also get the same result printing `europe.gdpPercap_1952` (not recommended, because easily confused with `.` notation for methods)

## Select multiple columns or rows using `DataFrame.loc` and a named slice.

```python
print(europe.loc['Italy':'Poland', 'gdpPercap_1962':'gdpPercap_1972'])
```

```output
             gdpPercap_1962  gdpPercap_1967  gdpPercap_1972
country
Italy           8243.582340    10022.401310    12269.273780
Montenegro      4649.593785     5907.850937     7778.414017
Netherlands    12790.849560    15363.251360    18794.745670
Norway         13450.401510    16361.876470    18965.055510
Poland          5338.752143     6557.152776     8006.506993
```

In the above code, we discover that **slicing using `loc` is inclusive at both
ends**, which differs from **slicing using `iloc`**, where slicing indicates
everything up to but not including the final index.

## Result of slicing can be used in further operations.

- Usually don't just print a slice.
- All the statistical operators that work on entire dataframes
  work the same way on slices.
- E.g., calculate max of a slice.

```python
print(europe.loc['Italy':'Poland', 'gdpPercap_1962':'gdpPercap_1972'].max())
```

```output
gdpPercap_1962    13450.40151
gdpPercap_1967    16361.87647
gdpPercap_1972    18965.05551
dtype: float64
```

```python
print(europe.loc['Italy':'Poland', 'gdpPercap_1962':'gdpPercap_1972'].min())
```

```output
gdpPercap_1962    4649.593785
gdpPercap_1967    5907.850937
gdpPercap_1972    7778.414017
dtype: float64
```

## Comparisons in Python return True or False

Let's introduce a simple Python data type that hasn't been explicitly introduced yet: the [**Boolean**](https://docs.python.org/3/library/stdtypes.html#boolean-operations-and-or-not) or `bool`.

- Booleans are either `True` or `False`. 
- Capitalization matters here! `true` is not a valid Boolean.

```python
type(True) # Notice how True changes color when capitalized
```

```output
bool
```

Booleans are returned when we test the **truth value** of a statement. To test whether two objects are equal, we use `==`. (This is different from the `=` used for assignment.)

```python
x = 5 # Assign x the value 5
print(x)
print(x == 10) # Is the value at x equal to 10, True or False
print(x == 5) # Is the value at x equal to 5, True or False
```

```output
5
False
True
```

Booleans are returned by statements that make numerical comparisons using operators like `>`, `<=` and `!=`.

- Try `!=`, which can be read as "is not equal to".

```python
5 != 3 #Is 5 equal to 3?
```

```output
False
```

- `<` is the "less than" operator.

```python
2 < 3
```

```output
True
```

You can also do comparisons between two variables.

```python
t_celsius = 0
t_farenheit = 32
t_celsius < t_farenheit # Evaluates to True or False
```

```output
True
```

## Use comparisons to select data based on value.

- Comparison is applied element by element.
- Returns a similarly-shaped dataframe of `True` and `False`.

```python
# Use a subset of data to keep output readable.
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

## Equals (`==`) is Not Equals (`=`)

There are many instances where `==` and `=` can **both** be used. What combination of `==` and `=` will make the statement in the second line print False? 

Replace `PICKASIGN` with either an `=` or `==`.

```python
is_the_sky_blue PICKASIGN "sky" PICKASIGN "blue"
print(is_the_sky_blue)
```

:::::::::::::::  solution

## Solution

Remember that `=` is used to assign a value to a variable, while `==` is a comparator. 

```python
is_the_sky_blue = "sky" == "blue"
print(is_the_sky_blue)
```
Solve the problem by comparing "sky" to "blue" with `==`, which evaluates to False, then assign False to
`is_the_sky_blue`. The second line will then print `False`.


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
- Booleans store truth values.
- Select values or NaN using a Boolean mask.

::::::::::::::::::::::::::::::::::::::::::::::::::



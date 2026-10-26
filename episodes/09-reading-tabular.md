---
title: Reading Tabular Data into DataFrames
teaching: 10
exercises: 10
---

::::::::::::::::::::::::::::::::::::::: objectives

- Import the Pandas library.
- Use Pandas to load a simple CSV data set.
- Get some basic information about a Pandas DataFrame.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- What is tabular data?
- How can I read tabular data in Python?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Pandas is a library for manipulating data

In previous lessons, you were introduced to modules from Python's [standard library](https://docs.python.org/3/library/index.html. Python also allows you to integrate libraries developed by third-party communities of developers.

This lesson introduces Pandas, an open-source library developed by NumFocus that you installed on the first day of the workhsop.

### What is Pandas?
* [Pandas](https://pandas.pydata.org/docs/user_guide/index.html) is a popular library for importing, managing, and manipulating tabular data.
* Pandas was inspired by R's dataframes.
* Pandas can read in data from many tabular formats including .csv files, .xlsx files, and relational database tables.
* We will use Pandas to read in CSV (comma-separated value) files.

### Version Check

First, check that you have Pandas installed.
```python
import pandas as pd # This alias is conventional
print(pd.__version__)
```
```output
3.0.6
```

:::::::::::::::::::::::::::::::::::::::::  callout

## Debugging Import Statements
Depending on when and how your Python environment
was created, you may encounter an
error when importing Pandas. Here are two
common problems and how to fix them.

### ModuleNotFoundError
If you get a **ModuleNotFoundError** when trying to import a third-party 
library like Pandas, that means the current [Python environment](https://blog.jupyter.org/python-environment-management-in-jupyterlab-desktop-3b119c5811d9)
does not have that library installed. 

Run this exactly once to prepare your environment. 
```python
!conda install pandas numpy matlplotlib -y
```


### ImportError: Unable to import required dependencies
If you get an **ImportError** that mentions numpy, you may
have an incompatibility problem in your Python environment.
Numpy is a dependency of Pandas, but some versions of Numpy are incompatible with
some versions of Pandas.
If you get an error referencing an incompatibility problem, reinstall
Pandas *and* its dependencies with the following
command.

```python
!conda update pandas numpy matlplotlib -y
```

Run this exactly once.


:::::::::::::::::::::::::::::::::::::::::::::

## Reading DataFrames from Files

To read in CSV files as DataFrames using Pandas, use the [**read_csv()**](https://pandas.pydata.org/docs/reference/api/pandas.read_csv.html) function.
  - The first argument is the name of the file to be read.
  - The function returns a DataFrame that you can assign to a variable

This is a peek of what a `gapminder_gdp_oceania.csv` looks like. As you can see, it's a comma-separated text file, with one line per row of data. The first row is special, as it gives the name of each column.
```output
	country	gdpPercap_1952	gdpPercap_1957	gdpPercap_1962	gdpPercap_1967	gdpPercap_1972	gdpPercap_1977	gdpPercap_1982	gdpPercap_1987	gdpPercap_1992	gdpPercap_1997	gdpPercap_2002	gdpPercap_2007
1	Australia	10039.59564	10949.64959	12217.22686	14526.12465	16788.62948	18334.19751	19477.00928	21888.88903	23424.76683	26997.93657	30687.75473	34435.36744
2	New Zealand	10556.57566	12247.39532	13175.678	14463.91893	16046.03728	16233.7177	17632.4104	19007.19129	18363.32494	21050.41377	23189.80135	25185.00911
```

To read in `gapminder_gdp_ocenia.csv`, you must supply its *path* relative to your **current working directory**. It should be in the `data` directory we created on the first day of class.
```python
gdp_oceania = pd.read_csv("data/gapminder_gdp_oceania.csv")
```

:::::::::::::::::::::::::::::::::::::::::  callout

## File Not Found

Our lessons store their data files in a `data` sub-directory,
which is why the path to the file is `data/gapminder_gdp_oceania.csv`.
If you forget to include `data/`,
or if you include it but your copy of the file is somewhere else,
you will get a [runtime error](04-built-in.md)
that ends with a line like this:

```error
FileNotFoundError: [Errno 2] No such file or directory: 'data/gapminder_gdp_oceania.csv'
```

::::::::::::::::::::::::::::::::::::::::::::::::::


Take a peek at the `gdp_oceania` DataFrame returned by `pd.read_csv`. A Pandas DataFrame is optimized to display in a human-readable format in a Jupyter Notebook, so you will see your data with bolded column names, just like a spreadsheet.

```python
gdp_oceania
```
```output
       country  gdpPercap_1952  gdpPercap_1957  gdpPercap_1962  \
0    Australia     10039.59564     10949.64959     12217.22686
1  New Zealand     10556.57566     12247.39532     13175.67800

   gdpPercap_1967  gdpPercap_1972  gdpPercap_1977  gdpPercap_1982  \
0     14526.12465     16788.62948     18334.19751     19477.00928
1     14463.91893     16046.03728     16233.71770     17632.41040

   gdpPercap_1987  gdpPercap_1992  gdpPercap_1997  gdpPercap_2002  \
0     21888.88903     23424.76683     26997.93657     30687.75473
1     19007.19129     18363.32494     21050.41377     23189.80135

   gdpPercap_2007
0     34435.36744
1     25185.00911
```

## A DataFrame has a shape and columns

The shape of a DataFrame is stored the `.shape` attribute in the form `(rows, columns`). Attributes are variables bound to specific objects, just like methods are bound to specific objects. Because attributes are variables rather than functions, you don't need to call them with `()`.

```python
gdp_oceania.shape # Prints the shape of DF in row, column form
```
```output
(2, 13)
```

We can get a list of those named columns using the `.columns` attribute.

```python
gdp_oceania.columns
```
```output
Index(['country', 'gdpPercap_1952', 'gdpPercap_1957', 'gdpPercap_1962',
       'gdpPercap_1967', 'gdpPercap_1972', 'gdpPercap_1977', 'gdpPercap_1982',
       'gdpPercap_1987', 'gdpPercap_1992', 'gdpPercap_1997', 'gdpPercap_2002',
       'gdpPercap_2007'],
      dtype='str')
```

We have read in a DataFrame with two rows and 13 columns. The first column is the name of a country, the following 12 represent GDP measurements in that country between 1952 and 2007.


## Use the `DataFrame.info()` method to find out more about a DataFrame

```python
gdp_oceania.info()
```
```output
<class 'pandas.DataFrame'>
RangeIndex: 2 entries, 0 to 1
Data columns (total 13 columns):
 #   Column          Non-Null Count  Dtype  
---  ------          --------------  -----  
 0   country         2 non-null      str    
 1   gdpPercap_1952  2 non-null      float64
 2   gdpPercap_1957  2 non-null      float64
 3   gdpPercap_1962  2 non-null      float64
 4   gdpPercap_1967  2 non-null      float64
 5   gdpPercap_1972  2 non-null      float64
 6   gdpPercap_1977  2 non-null      float64
 7   gdpPercap_1982  2 non-null      float64
 8   gdpPercap_1987  2 non-null      float64
 9   gdpPercap_1992  2 non-null      float64
 10  gdpPercap_1997  2 non-null      float64
 11  gdpPercap_2002  2 non-null      float64
 12  gdpPercap_2007  2 non-null      float64
dtypes: float64(12), str(1)
memory usage: 340.0 bytes
```

Every column in a DataFrame has an assigned data type that specifies what types of values can be in that column. This information is inferred when data is read in from a file by Pandas.

## Use `index_col` to specify that a column's values should be used to name rows
Both columns and rows in a DataFrame have names. We can look at the row names in the `.index` attribute. Row names will default to a RangeIndex starting at 0 and stopping at num_rows - 1.

```python
gdp_oceania.index
```
```output
RangeIndex(start=0, stop=2, step=1)
```

What if we want to name each row by `country` instead? We can do this by passing the name of the column to `read_csv` as its `index_col`. This is called a **keyword argument**. Keyword arguments are optional and listed in `parameter_name=argument` form.

Let's create a new DataFrame called `oceania_country` that is indexed by `country` instead.
```python
oceania_country = pd.read_csv('data/gapminder_gdp_oceania.csv', index_col='country')
oceania_country
```
```output
             gdpPercap_1952  gdpPercap_1957  gdpPercap_1962  gdpPercap_1967  \
country
Australia       10039.59564     10949.64959     12217.22686     14526.12465
New Zealand     10556.57566     12247.39532     13175.67800     14463.91893

             gdpPercap_1972  gdpPercap_1977  gdpPercap_1982  gdpPercap_1987  \
country
Australia       16788.62948     18334.19751     19477.00928     21888.88903
New Zealand     16046.03728     16233.71770     17632.41040     19007.19129

             gdpPercap_1992  gdpPercap_1997  gdpPercap_2002  gdpPercap_2007
country
Australia       23424.76683     26997.93657     30687.75473     34435.36744
New Zealand     18363.32494     21050.41377     23189.80135     25185.00911
```

## Use `DataFrame.T` to transpose a DataFrame.

Sometimes we want to treat columns as rows and vice versa.
Transpose (written `.T`) stores this in a special attribute. It does not change the original DataFrame.

```python
oceania_country.T
```
```output
country 	Australia 	New Zealand
gdpPercap_1952 	10039.59564 	10556.57566
gdpPercap_1957 	10949.64959 	12247.39532
gdpPercap_1962 	12217.22686 	13175.678
gdpPercap_1967 	14526.12465 	14463.91893
gdpPercap_1972 	16788.62948 	16046.03728
gdpPercap_1977 	18334.19751 	16233.7177
gdpPercap_1982 	19477.00928 	17632.4104
gdpPercap_1987 	21888.88903 	19007.19129
gdpPercap_1992 	23424.76683 	18363.32494
gdpPercap_1997 	26997.93657 	21050.41377
gdpPercap_2002 	30687.75473 	23189.80135
gdpPercap_2007 	34435.36744 	25185.00911
```

## Use `DataFrame.describe()` to get summary statistics about data.

`DataFrame.describe()` gets the summary statistics of only the columns that have numerical data.
All other columns are ignored, unless you use the argument `include='all'`.

```python
oceania_country.describe()
```

```output
 	gdpPercap_1952 	gdpPercap_1957 	gdpPercap_1962 	gdpPercap_1967 	gdpPercap_1972 	gdpPercap_1977 	gdpPercap_1982 	gdpPercap_1987 	gdpPercap_1992 	gdpPercap_1997 	gdpPercap_2002 	gdpPercap_2007
count 	2.000000 	2.000000 	2.000000 	2.000000 	2.00000 	2.000000 	2.000000 	2.000000 	2.000000 	2.000000 	2.000000 	2.000000
mean 	10298.085650 	11598.522455 	12696.452430 	14495.021790 	16417.33338 	17283.957605 	18554.709840 	20448.040160 	20894.045885 	24024.175170 	26938.778040 	29810.188275
std 	365.560078 	917.644806 	677.727301 	43.986086 	525.09198 	1485.263517 	1304.328377 	2037.668013 	3578.979883 	4205.533703 	5301.853680 	6540.991104
min 	10039.595640 	10949.649590 	12217.226860 	14463.918930 	16046.03728 	16233.717700 	17632.410400 	19007.191290 	18363.324940 	21050.413770 	23189.801350 	25185.009110
25% 	10168.840645 	11274.086022 	12456.839645 	14479.470360 	16231.68533 	16758.837652 	18093.560120 	19727.615725 	19628.685412 	22537.294470 	25064.289695 	27497.598692
50% 	10298.085650 	11598.522455 	12696.452430 	14495.021790 	16417.33338 	17283.957605 	18554.709840 	20448.040160 	20894.045885 	24024.175170 	26938.778040 	29810.188275
75% 	10427.330655 	11922.958888 	12936.065215 	14510.573220 	16602.98143 	17809.077558 	19015.859560 	21168.464595 	22159.406358 	25511.055870 	28813.266385 	32122.777858
max 	10556.575660 	12247.395320 	13175.678000 	14526.124650 	16788.62948 	18334.197510 	19477.009280 	21888.889030 	23424.766830 	26997.936570 	30687.754730 	34435.367440
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Reading Other Data

Read the data in `gapminder_gdp_americas.csv`
(which should be in the same directory as `gapminder_gdp_oceania.csv`)
into a variable called `data_americas`
and display its summary statistics.

:::::::::::::::  solution

## Solution

To read in a CSV, we use `pd.read_csv` and pass the filename `'data/gapminder_gdp_americas.csv'` to it.
We also once again pass the column name `'country'` to the parameter `index_col` in order to index by country.
The summary statistics can be displayed with the `DataFrame.describe()` method.

```python
data_americas = pd.read_csv('data/gapminder_gdp_americas.csv', index_col='country')
data_americas.describe()
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Inspecting Data

After reading the data for the Americas,
use `help(data_americas.head)` and `help(data_americas.tail)`
to find out what `DataFrame.head` and `DataFrame.tail` do.

1. What method call will display the first three rows of this data?
2. What method call will display the last three columns of this data?
  (Hint: you may need to change your view of the data.)

:::::::::::::::  solution

## Solution

1. We can check out the first five rows of `data_americas` by executing `data_americas.head()`
  which lets us view the beginning of the DataFrame. We can specify the number of rows we wish
  to see by specifying the parameter `n` in our call to `data_americas.head()`.
  To view the first three rows, execute:
  
  ```python
  data_americas.head(n=3)
  ```
  
  ```output
            continent  gdpPercap_1952  gdpPercap_1957  gdpPercap_1962  \
  country
  Argentina  Americas     5911.315053     6856.856212     7133.166023
  Bolivia    Americas     2677.326347     2127.686326     2180.972546
  Brazil     Americas     2108.944355     2487.365989     3336.585802
  
            gdpPercap_1967  gdpPercap_1972  gdpPercap_1977  gdpPercap_1982  \
  country
  Argentina     8052.953021     9443.038526    10079.026740     8997.897412
  Bolivia       2586.886053     2980.331339     3548.097832     3156.510452
  Brazil        3429.864357     4985.711467     6660.118654     7030.835878
  
             gdpPercap_1987  gdpPercap_1992  gdpPercap_1997  gdpPercap_2002  \
  country
  Argentina     9139.671389     9308.418710    10967.281950     8797.640716
  Bolivia       2753.691490     2961.699694     3326.143191     3413.262690
  Brazil        7807.095818     6950.283021     7957.980824     8131.212843
  
             gdpPercap_2007
  country
  Argentina    12779.379640
  Bolivia       3822.137084
  Brazil        9065.800825
  ```

2. To check out the last three rows of `data_americas`, we would use the command,
  `americas.tail(n=3)`, analogous to `head()` used above. However, here we want to look at
  the last three columns so we need to change our view and then use `tail()`. To do so, we
  create a new DataFrame in which rows and columns are switched:
  
  ```python
  americas_flipped = data_americas.T
  ```
  
  We can then view the last three columns of `americas` by viewing the last three rows
  of `americas_flipped`:
  
  ```python
  americas_flipped.tail(n=3)
  ```
  
  ```output
  country        Argentina  Bolivia   Brazil   Canada    Chile Colombia  \
  gdpPercap_1997   10967.3  3326.14  7957.98  28954.9  10118.1  6117.36
  gdpPercap_2002   8797.64  3413.26  8131.21    33329  10778.8  5755.26
  gdpPercap_2007   12779.4  3822.14   9065.8  36319.2  13171.6  7006.58
  
  country        Costa Rica     Cuba Dominican Republic  Ecuador    ...     \
  gdpPercap_1997    6677.05  5431.99             3614.1  7429.46    ...
  gdpPercap_2002    7723.45  6340.65            4563.81  5773.04    ...
  gdpPercap_2007    9645.06   8948.1            6025.37  6873.26    ...
  
  country          Mexico Nicaragua   Panama Paraguay     Peru Puerto Rico  \
  gdpPercap_1997   9767.3   2253.02  7113.69   4247.4  5838.35     16999.4
  gdpPercap_2002  10742.4   2474.55  7356.03  3783.67  5909.02     18855.6
  gdpPercap_2007  11977.6   2749.32  9809.19  4172.84  7408.91     19328.7
  
  country        Trinidad and Tobago United States  Uruguay Venezuela
  gdpPercap_1997             8792.57       35767.4  9230.24   10165.5
  gdpPercap_2002             11460.6       39097.1     7727   8605.05
  gdpPercap_2007             18008.5       42951.7  10611.5   11415.8
  ```
  
  This shows the data that we want, but we may prefer to display three columns instead of three rows,
  so we can flip it back:
  
  ```python
  americas_flipped.tail(n=3).T    
  ```
  
  **Note:** we could have done the above in a single line of code by 'chaining' the commands:
  
  ```python
  data_americas.T.tail(n=3).T
  ```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Reading Files in Other Directories

Imagine that the data for your current project is stored in a file called `microbes.csv`,
which is located in a folder called `field_data`.
You are doing analysis in a notebook called `analysis.ipynb`
in a sibling folder called `thesis`:

```output
your_home_directory
+-- field_data/
|   +-- microbes.csv
+-- thesis/
    +-- analysis.ipynb
```

What value(s) should you pass to `read_csv` to read `microbes.csv` in `analysis.ipynb`?

:::::::::::::::  solution

## Solution

We need to specify the path to the file of interest in the call to `pd.read_csv`. We first need to 'jump' out of
the folder `thesis` using '../' and then into the folder `field_data` using 'field\_data/'. Then we can specify the filename \`microbes.csv.
The result is as follows:

```python
data_microbes = pd.read_csv('../field_data/microbes.csv')
```

:::::::::::::::::::::::::


::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Writing Data

As well as the `read_csv` function for reading data from a file,
Pandas provides a `to_csv` function to write DataFrames to files.
Applying what you've learned about reading from files,
write one of your DataFrames to a file called `processed.csv`.
You can use `help` to get information on how to use `to_csv`.

:::::::::::::::  solution

## Solution

In order to write the DataFrame `data_americas` to a file called `processed.csv`, execute the following command:

```python
data_americas.to_csv('processed.csv')
```

For help on `read_csv` or `to_csv`, you could execute, for example:

```python
help(data_americas.to_csv)
help(pd.read_csv)
```

Note that `help(to_csv)` or `help(pd.to_csv)` throws an error! This is due to the fact that `to_csv` is not a global Pandas function, but
a member function of DataFrames. This means you can only call it on an instance of a DataFrame
e.g., `data_americas.to_csv` or `data_oceania.to_csv`



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Use the Pandas library to get basic statistics out of tabular data.
- Use `index_col` to specify that a column's values should be used as row headings.
- Use `DataFrame.info` to find out more about DataFrame.
- The `DataFrame.columns` variable stores information about the DataFrame's columns.
- Use `DataFrame.T` to transpose a DataFrame.
- Use `DataFrame.describe` to get summary statistics about data.

::::::::::::::::::::::::::::::::::::::::::::::::::



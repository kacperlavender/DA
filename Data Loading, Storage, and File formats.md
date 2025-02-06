#### Text and binary data loading functions in pandas
| Function          | Description |
|------------------|----------------------------------------------------------------|
| `read_csv`       | Load delimited data from a file, URL, or file-like object; uses comma as the default delimiter. |
| `read_fwf`       | Read data in fixed-width column format (i.e., no delimiters). |
| `read_clipboard` | Variation of `read_csv` that reads data from the clipboard; useful for converting tables from web pages. |
| `read_excel`     | Read tabular data from an Excel XLS or XLSX file. |
| `read_hdf`       | Read HDF5 files written by pandas. |
| `read_html`      | Read all tables found in the given HTML document. |
| `read_json`      | Read data from a JSON string, file, URL, or file-like object. |
| `read_feather`   | Read the Feather binary file format. |
| `read_orc`       | Read the Apache ORC binary file format. |
| `read_parquet`   | Read the Apache Parquet binary file format. |
| `read_pickle`    | Read an object stored by pandas using the Python pickle format. |
| `read_sas`       | Read a SAS dataset stored in one of SAS system’s custom storage formats. |
| `read_spss`      | Read a data file created by SPSS. |
| `read_sql`       | Read the results of a SQL query (using SQLAlchemy). |
| `read_sql_table` | Read a whole SQL table (using SQLAlchemy); equivalent to selecting everything using `read_sql`. |
| `read_stata`     | Read a dataset from Stata file format. |
| `read_xml`       | Read a table of data from an XML file. |

Overview of the mechanics of these functions, which are meant to convert text data into a DataFrame. The optional arguments for these functions may fall into a few categories:
Indexing
	Can treat one or more columns as the returned DataFrame, and whether to get column names from the file, arguments you provide, or not at all.
Type inference and data conversion
	Includes the user-defined value conversions and custom list of missing value markers.
Date and time parsing
	Includes a combining capability, including combining date and time information spread over multiple columns into a single column in the result.
Iterating
	Support for iterating over chunks of very large files.
Unclean data issues
	Includes skipping rows or a footer, comments, or other minor things like numeric data with thousands separated by commas


Because of how messy data in the real world can be, some of the data loading functions (especially pandas.read_csv) have accumulated a long list of optional arguments over time. It’s normal to feel overwhelmed by the number of different parameters (pandas.read_csv has around 50). The online pandas documentation has many examples about how each of these works, so if you’re struggling to read a particular file, there might be a similar enough example to help you find the right parameters.



A file will not always have a header row. Consider this file:
```python
In [40]: pd.read_csv(r"examples\ex2.csv")
Out[40]:
   1   2   3   4  hello
0  5   6   7   8  world
1  9  10  11  12    foo
```
To read this file, you have a couple of options. You can allow pandas to assign default column names, or you can specify names yourself:
```python
In [41]: pd.read_csv(r"examples\ex2.csv", header=None)
Out[41]:
   0   1   2   3      4
0  1   2   3   4  hello
1  5   6   7   8  world
2  9  10  11  12    foo

In [42]: pd.read_csv(r"examples\ex2.csv", names=["a", "b", "c", "d", "message"])
Out[42]:
   a   b   c   d message
0  1   2   3   4   hello
1  5   6   7   8   world
2  9  10  11  12     foo
```


```python
In [15]: !cat examples/ex4.csv
# hey!
a,b,c,d,message
# just wanted to make things more difficult for you
# who reads CSV files with computers, anyway?
1,2,3,4,hello
5,6,7,8,world
9,10,11,12,foo

In [16]: pd.read_csv("examples/ex4.csv", skiprows=[0,2,3])
Out[16]:
   a   b   c   d message
0  1   2   3   4   hello
1  5   6   7   8   world
2  9  10  11  12     foo
```

####  Some `pandas.read_csv` function arguments

| Argument             | Description                                                                                                                                                                                                                                                                                                       |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `path`               | String indicating filesystem location, URL, or file-like object.                                                                                                                                                                                                                                                  |
| `sep` or `delimiter` | Character sequence or regular expression to use to split fields in each row.                                                                                                                                                                                                                                      |
| `header`             | Row number to use as column names; defaults to `0` (first row), but should be `None` if there is no header row.                                                                                                                                                                                                   |
| `index_col`          | Column numbers or names to use as the row index in the result; can be a single name/number or a list of them for a hierarchical index.                                                                                                                                                                            |
| `names`              | List of column names for result.                                                                                                                                                                                                                                                                                  |
| `skiprows`           | Number of rows at the beginning of the file to ignore, or list of row numbers (starting from `0`) to skip.                                                                                                                                                                                                        |
| `na_values`          | Sequence of values to replace with `NA`. They are added to the default list unless `keep_default_na=False` is passed.                                                                                                                                                                                             |
| `keep_default_na`    | Whether to use the default `NA` value list or not (`True` by default).                                                                                                                                                                                                                                            |
| `comment`            | Character(s) to split comments off the end of lines.                                                                                                                                                                                                                                                              |
| `parse_dates`        | Attempt to parse data to datetime; `False` by default. If `True`, will attempt to parse all columns. Otherwise, specify a list of column numbers or names to parse. If a list element is a tuple or list, will combine multiple columns together and parse to date (e.g., if date/time split across two columns). |
| `keep_date_col`      | If joining columns to parse date, keep the joined columns; `False` by default.                                                                                                                                                                                                                                    |
| `converters`         | Dictionary mapping column numbers or names to functions (e.g., `{"foo": f}` applies function `f` to all values in the `"foo"` column).                                                                                                                                                                            |
| `dayfirst`           | When parsing ambiguous dates, treat as international format (e.g., `7/6/2012 -> June 7, 2012`); `False` by default.                                                                                                                                                                                               |
| `date_parser`        | Function to use to parse dates.                                                                                                                                                                                                                                                                                   |
| `nrows`              | Number of rows to read from the beginning of the file (excluding the header).                                                                                                                                                                                                                                     |
| `iterator`           | Return a `TextFileReader` object for reading the file piecemeal. This object can also be used with the `with` statement.                                                                                                                                                                                          |
| `chunksize`          | For iteration, size of file chunks.                                                                                                                                                                                                                                                                               |
| `skip_footer`        | Number of lines to ignore at the end of the file.                                                                                                                                                                                                                                                                 |
| `verbose`            | Print parsing information, such as time spent in each stage of file conversion and memory use details.                                                                                                                                                                                                            |
| `encoding`           | Text encoding (e.g., `"utf-8"` for UTF-8 encoded text). Defaults to `"utf-8"` if `None`.                                                                                                                                                                                                                          |
| `squeeze`            | If the parsed data contains only one column, return a `Series`.                                                                                                                                                                                                                                                   |
| `thousands`          | Separator for thousands (e.g., `","` or `"."`); default is `None`.                                                                                                                                                                                                                                                |
| `decimal`            | Decimal separator in numbers (e.g., `"."` or `","`); default is `"."`.                                                                                                                                                                                                                                            |
| `engine`             | CSV parsing and conversion engine to use; can be `"c"`, `"python"`, or `"pyarrow"`. The default is `"c"`, though `"pyarrow"` can parse some files much faster. The `"python"` engine is slower but supports features the others do not.                                                                           |


### Reading Text Files in Pieces
When processing very large files or figuring out the right set of arguments to correctly process a large file, you may want to read only a small piece of a file or iterate through smaller chunks of the file.

```python
In [18]: pd.options.display.max_rows = 10
```


#### Working with Other Delimited Formats
```python
In [32]: import csv

In [33]: f = open("examples/ex7.csv")

In [34]: reader = csv.reader(f)

In [35]: for line in reader:
    ...:     print(line)
    ...:
['a', 'b', 'c']
['1', '2', '3']
['1', '2', '3']

In [36]: f.close()
```

#### CSV dialect options
| Argument           | Description                                                                                                                                                                                                                                   |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `delimiter`        | One-character string to separate fields; defaults to `","`.                                                                                                                                                                                   |
| `lineterminator`   | Line terminator for writing; defaults to `"\r\n"`. Reader ignores this and recognizes cross-platform line terminators.                                                                                                                        |
| `quotechar`        | Quote character for fields with special characters (like a delimiter); default is `"'"`.                                                                                                                                                      |
| `quoting`          | Quoting convention. Options include `csv.QUOTE_ALL` (quote all fields), `csv.QUOTE_MINIMAL` (only fields with special characters like the delimiter), `csv.QUOTE_NONNUMERIC`, and `csv.QUOTE_NONE` (no quoting). Defaults to `QUOTE_MINIMAL`. |
| `skipinitialspace` | Ignore whitespace after each delimiter; default is `False`.                                                                                                                                                                                   |
| `doublequote`      | How to handle quoting character inside a field; if `True`, it is doubled (see online documentation for full detail and behavior).                                                                                                             |
| `escapechar`       | String to escape the delimiter if quoting is set to `csv.QUOTE_NONE`; disabled by default.                                                                                                                                                    |

### Filling In Missing Data
Rather than filtering out missing data (and potentially discarding other data along with it), you may want to fill in the “holes” in any number of ways. For most purposes, the fillna method is the workhorse function to use. Calling fillna with a constant replaces missing values with that value:
```python
In [37]: df = pd.DataFrame(np.random.standard_normal((7, 3)))

In [38]: df.fillna(0)
Out[38]:
          0         1         2
0 -0.935806 -0.048369 -1.284787
1  0.448303 -1.069325  0.812073
2  0.082863 -0.141884 -0.023553
3 -1.201179  0.591698 -0.567232
4 -0.240314 -0.133325  0.124686
5 -0.558235  1.269327  1.304039
6 -1.148401 -0.340334  1.299756
```

Calling `fillna` with a dictionary, you can use a different fill value for each column:
```python
In [39]: df.fillna({1: 0.5, 2: 0})
Out[39]:
          0         1         2
0 -0.935806 -0.048369 -1.284787
1  0.448303 -1.069325  0.812073
2  0.082863 -0.141884 -0.023553
3 -1.201179  0.591698 -0.567232
4 -0.240314 -0.133325  0.124686
5 -0.558235  1.269327  1.304039
6 -1.148401 -0.340334  1.299756
```

With fillna you can do lots of other things such as simple data imputation using the median or mean statistics:
```python
In [45]: data = pd.Series([1., np.nan, 3.5, np.nan, 7])

In [46]: data.fillna(data.mean())
Out[46]:
0    1.000000
1    3.833333
2    3.500000
3    3.833333
4    7.000000
dtype: float64
```
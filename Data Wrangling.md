### Hierarchical Indexing
Hierarchical indexing is an important feature of pandas that enables you to have multiple (two or more) index levels on an axis. Another way of thinking about it is that it provides a way for you to work with higher dimensional data in a lower dimensional form. Let’s start with a simple example: create a Series with a list of lists (or arrays) as the index:
```python
In [74]: data = pd.Series(np.random.uniform(size=9), 
						index=[["a", "a", "a", "b", "b", "c", "c", "d", "d"],
						[1, 2, 3, 1, 3, 1, 2, 2, 3]])

In [75]: data
Out[75]:
a  1    0.747715
   2    0.961307
   3    0.008388
b  1    0.106444
   3    0.298704
c  1    0.656411
   2    0.809813
d  2    0.872176
   3    0.964648
dtype: float64
```

```python
In [78]: frame = pd.DataFrame(np.arange(12).reshape((4, 3)),
    ...: ....: index=[["a", "a", "b", "b"], [1, 2, 1, 2]],
    ...: ....: columns=[["Ohio", "Ohio", "Colorado"],
    ...: ....: ["Green", "Red", "Green"]])

In [79]: frame
Out[79]:
     Ohio     Colorado
    Green Red    Green
a 1     0   1        2
  2     3   4        5
b 1     6   7        8
  2     9  10       11
```


### Indexing with a DataFrame’s columns
It’s not unusual to want to use one or more columns from a DataFrame as the row index; alternatively, you may wish to move the row index into the DataFrame’s columns. Here’s an example DataFrame:
```python
In [80]: frame = pd.DataFrame({"a": range(7), "b": range(7, 0, -1),
    ...: ....: "c": ["one", "one", "one", "two", "two",
    ...: ....: "two", "two"],
    ...: ....: "d": [0, 1, 2, 0, 1, 2, 3]})

In [81]: frame
Out[81]:
   a  b    c  d
0  0  7  one  0
1  1  6  one  1
2  2  5  one  2
3  3  4  two  0
4  4  3  two  1
5  5  2  two  2
6  6  1  two  3

In [82]: frame2 = frame.set_index(["c", "d"])

In [83]: frame2
Out[84]:
       a  b
c   d
one 0  0  7
    1  1  6
    2  2  5
two 0  3  4
    1  4  3
    2  5  2
    3  6  1
```


### Combining and Merging Datasets
pandas.merge
	Connect rows in DataFrames based on one or more keys. This will be familiar to users of SQL or other relational databases, as it implements database join operations.
pandas.concat
	Concatenate or “stack” objects together along an axis.
combine_first
	Splice together overlapping data to fill in missing values in one object with values from another.

```python
In [85]: df1 = pd.DataFrame({"key": ["b", "b", "a", "c", "a", "a", "b"],
    ...: ....: "data1": pd.Series(range(7), dtype="Int64")})

In [86]: df2 = pd.DataFrame({"key": ["a", "b", "d"],
    ...: ....: "data2": pd.Series(range(3), dtype="Int64")})

In [87]: df1
Out[87]:
  key  data1
0   b      0
1   b      1
2   a      2
3   c      3
4   a      4
5   a      5
6   b      6

In [88]: df2
Out[88]:
  key  data2
0   a      0
1   b      1
2   d      2

In [89]: pd.merge(df1, df2)
Out[89]:
  key  data1  data2
0   b      0      1
1   b      1      1
2   a      2      0
3   a      4      0
4   a      5      0
5   b      6      1
```

Note that I didn’t specify which column to join on. If that information is not specified, pandas.merge uses the overlapping column names as the keys. It’s a good practice to specify explicitly, though:
`pd.merge(df1, df2, on="key")`



#### Different join types with the how argument

| Option          | Behavior                                                  |
| --------------- | --------------------------------------------------------- |
| **how="inner"** | Use only the key combinations observed in both tables     |
| **how="left"**  | Use all key combinations found in the left table          |
| **how="right"** | Use all key combinations found in the right table         |
| **how="outer"** | Use all key combinations observed in both tables together |

### pandas.merge function arguments
| Argument      | Description |
|--------------|-----------------------------------------------------------|
| **left**     | DataFrame to be merged on the left side. |
| **right**    | DataFrame to be merged on the right side. |
| **how**      | Type of join to apply: "inner", "outer", "left", or "right"; defaults to "inner". |
| **on**       | Column names to join on. If not specified, uses the intersection of column names in both DataFrames. |
| **left_on**  | Columns in left DataFrame to use as join keys. Can be a single column name or a list. |
| **right_on** | Analogous to left_on for right DataFrame. |
| **left_index**  | Use row index in left as its join key (or keys, if MultiIndex). |
| **right_index** | Analogous to left_index. |
| **sort**     | Sort merged data lexicographically by join keys; False by default. |
| **suffixes** | Tuple of suffixes to append to overlapping column names; defaults to ("_x", "_y"). |
| **copy**     | If False, avoids copying data in some cases; by default always copies. |
| **validate** | Verifies if the merge is one-to-one, one-to-many, or many-to-many. |
| **indicator** | Adds a column `_merge` indicating the origin of each row: "left_only", "right_only", or "both". |

#### pandas.concat function arguments
| Argument          | Description |
|------------------|--------------------------------------------------------------|
| **objs**        | List or dictionary of pandas objects to concatenate (required). |
| **axis**        | Axis to concatenate along; defaults to rows (`axis="index"`). |
| **join**        | Either `"inner"` or `"outer"` (`"outer"` by default); whether to intersect (inner) or union (outer) indexes along other axes. |
| **keys**        | Values to associate with objects, forming a hierarchical index along the concatenation axis. Can be a list, array, or tuples. |
| **levels**      | Specific indexes to use as hierarchical index level(s) if `keys` are passed. |
| **names**       | Names for hierarchical levels if `keys` and/or `levels` are passed. |
| **verify_integrity** | Checks for duplicates in the new axis and raises an exception if found; default is `False`. |
| **ignore_index** | If `True`, does not preserve indexes along the concatenation axis, instead creating a new range index. |

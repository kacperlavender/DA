### Arithmetic and Data Alignment
pandas can make it much simpler to work with objects that have different indexes. For example, when you add objects, if any index pairs are not the same, the respective index in the result will be the union of the index pairs.


#### Flexible arithmetic methods
| Method             | Description                      |
|--------------------|----------------------------------|
| `add`, `radd`     | Methods for addition (`+`)      |
| `sub`, `rsub`     | Methods for subtraction (`-`)   |
| `div`, `rdiv`     | Methods for division (`/`)      |
| `floordiv`, `rfloordiv` | Methods for floor division (`//`) |
| `mul`, `rmul`     | Methods for multiplication (`*`) |
| `pow`, `rpow`     | Methods for exponentiation (`**`) |

### Function Application and Mapping
```python
In [6]: frame = pd.DataFrame(np.random.standard_normal((4, 3)),
   ...: columns=list("bde"),
   ...: index=["Utah", "Ohio", "Texas", "Oregon"])

In [7]: frame
Out[7]:
               b         d         e
Utah    0.870011  0.123533  0.167659
Ohio   -0.312246  0.065934  1.155503
Texas  -0.995829  2.090423 -0.668255
Oregon  0.024819 -1.978131  0.805566

In [8]: np.abs(frame)
Out[8]:
               b         d         e
Utah    0.870011  0.123533  0.167659
Ohio    0.312246  0.065934  1.155503
Texas   0.995829  2.090423  0.668255
Oregon  0.024819  1.978131  0.805566

```


#### Sorting and Ranking
Sorting a dataset by some criterion is another important built-in operation. To sort lexicographically by row or column label, use the sort_index method, which returns a new, sorted object:
```python
In [10]: obj = pd.Series(np.arange(4), index=["d", "a", "b", "c"])

In [11]: obj.sort_index()
Out[11]:
a    1
b    2
c    3
d    0
dtype: int64

In [12]:
```
With a DataFrame, you can sort by index on either axis:
```python
In [12]: frame = pd.DataFrame(np.arange(8).reshape((2, 4)),
    ...: .....: index=["three", "one"],
    ...: .....: columns=["d", "a", "b", "c"])

In [13]: frame
Out[13]:
       d  a  b  c
three  0  1  2  3
one    4  5  6  7

In [14]: frame.sort_index()
Out[14]:
       d  a  b  c
one    4  5  6  7
three  0  1  2  3

In [15]: frame.sort_index(axis="columns")
Out[15]:
       a  b  c  d
three  1  2  3  0
one    5  6  7  4
```

The data is sorted in ascending order by default but can be sorted in descending order, too:
```python
In [16]: frame.sort_index(axis="columns", ascending=False)
Out[16]:
       d  c  b  a
three  0  3  2  1
one    4  7  6  5
```

Ranking assigns ranks from one through the number of valid data points in an array, starting from the lowest value. The rank methods for Series and DataFrame are the place to look; by default, rank breaks ties by assigning each group the mean rank:
```python
In [17]: obj = pd.Series([7, -5, 7, 4, 2, 0, 4])

In [18]: obj.rank()
Out[18]:
0    6.5
1    1.0
2    6.5
3    4.5
4    3.0
5    2.0
6    4.5
dtype: float64
```


### Tie-breaking methods with rank

| Method    | Description |
|-----------|-------------|
| `"average"` | Default: assign the average rank to each entry in the equal group. |
| `"min"`     | Use the minimum rank for the whole group. |
| `"max"`     | Use the maximum rank for the whole group. |
| `"first"`   | Assign ranks in the order the values appear in the data. |
| `"dense"`   | Like `method="min"`, but ranks always increase by 1 between groups rather than by the number of equal elements in a group. |


#### Axis Indexes with Duplicate Labels
Up until now almost all of the examples we have looked at have unique axis labels (index values). While many pandas functions (like reindex) require that the labels be unique, it’s not mandatory. Let’s consider a small Series with duplicate indices:
```python
In [19]: obj = pd.Series(np.arange(5), index=["a", "a", "b", "b", "c"])

In [20]: obj
Out[20]:
a    0
a    1
b    2
b    3
c    4
dtype: int64

In [21]: obj.index.is_unique
Out[21]: False

In [22]:
```


#### Summarizing and Computing Descriptive Statistics
pandas objects are equipped with a set of common mathematical and statistical methods. Most of these fall into the category of reductions or summary statistics, methods that extract a single value (like the sum or mean) from a Series, or a Series of values from the rows or columns of a DataFrame. Compared with the similar methods found on NumPy arrays, they have built-in handling for missing data. Consider a small DataFrame:
```python
In [28]: df = pd.DataFrame([[1.4, np.nan], [7.1, -4.5],
    ...: .....: [np.nan, np.nan], [0.75, -1.3]],
    ...: .....: index=["a", "b", "c", "d"],
    ...: .....: columns=["one", "two"])

In [29]: df
Out[29]:
    one  two
a  1.40  NaN
b  7.10 -4.5
c   NaN  NaN
d  0.75 -1.3

In [30]: df.sum()
Out[30]:
one    9.25
two   -5.80
dtype: float64

In [31]: df.sum(axis="columns")
Out[31]:
a    1.40
b    2.60
c    0.00
d   -0.55
dtype: float64
```


#### Options for reducing methods
| Method   | Description |
|----------|---------------------------------------------------------------|
| `axis`   | Axis to reduce over; `"index"` for DataFrame’s rows and `"columns"` for columns. |
| `skipna` | Exclude missing values; `True` by default. |
| `level`  | Reduce grouped by level if the axis is hierarchically indexed (MultiIndex). |

Some methods are neither reductions nor accumulations. describe is one such example, producing multiple summary statistics in one shot:
```python
In [34]: df.describe()
Out[34]:
            one       two
count  3.000000  2.000000
mean   3.083333 -2.900000
std    3.493685  2.262742
min    0.750000 -4.500000
25%    1.075000 -3.700000
50%    1.400000 -2.900000
75%    4.250000 -2.100000
max    7.100000 -1.300000
```


#### Descriptive and summary statistics

| Method             | Description                                                                                                                         |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------- |
| `count`            | Number of non-NA values.                                                                                                            |
| `describe`         | Compute set of summary statistics.                                                                                                  |
| `min`, `max`       | Compute minimum and maximum values.                                                                                                 |
| `argmin`, `argmax` | Compute index locations (integers) at which minimum or maximum value is obtained, respectively; not available on DataFrame objects. |
| `idxmin`, `idxmax` | Compute index labels at which minimum or maximum value is obtained, respectively.                                                   |
| `quantile`         | Compute sample quantile ranging from 0 to 1 (default: `0.5`).                                                                       |
| `sum`              | Sum of values.                                                                                                                      |
| `mean`             | Mean of values.                                                                                                                     |
| `median`           | Arithmetic median (50% quantile) of values.                                                                                         |
| `mad`              | Mean absolute deviation from mean value.                                                                                            |
| `prod`             | Product of all values.                                                                                                              |
| `var`              | Sample variance of values.                                                                                                          |
| `std`              | Sample standard deviation of values.                                                                                                |
| `skew`             | Sample skewness (third moment) of values.                                                                                           |
| `kurt`             | Sample kurtosis (fourth moment) of values.                                                                                          |
| `cumsum`           | Cumulative sum of values.                                                                                                           |
| `cummin`, `cummax` | Cumulative minimum or maximum of values, respectively.                                                                              |
| `cumprod`          | Cumulative product of values.                                                                                                       |
| `diff`             | Compute first arithmetic difference (useful for time series).                                                                       |
| `pct_change`       | Compute percent changes.                                                                                                            |

##### Unique, value counts, and set membership methods
| Method         | Description |
|---------------|---------------------------------------------------------------|
| `isin`        | Compute a Boolean array indicating whether each Series or DataFrame value is contained in the passed sequence of values. |
| `get_indexer` | Compute integer indices for each value in an array into another array of distinct values; helpful for data alignment and join-type operations. |
| `unique`      | Compute an array of unique values in a Series, returned in the order observed. |
| `value_counts` | Return a Series containing unique values as its index and frequencies as its values, ordered by count in descending order. |

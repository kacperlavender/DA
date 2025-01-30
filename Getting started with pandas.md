#### Series
A series is a one-dimensional array-like object containing sequence of values of the same type and associated array of data labels, called its *index*. Series if formed from only an array od data:
```
In [14]: obj = pd.Series([4, 7, -5, 3])

In [15]: obj
Out[15]:
0 4
1 7
2 -5
3 3
dtype: int64
```

Often, you’ll want to create a Series with an index identifying each data point with a label:
```
In [18]: obj2 = pd.Series([4, 7, -5, 3], index=["d", "b", "a", "c"])

In [19]: obj2
Out[19]:
d 4
b 7
a -5
c 3
dtype: int64

In [20]: obj2.index
Out[20]: Index(['d', 'b', 'a', 'c'], dtype='object')
```


Using NumPy functions or NumPy-like operations, such as filtering with a Boolean array, scalar multiplication, or applying math functions, will preserve the index-value link:
```
In [24]: obj2[obj2 > 0]
Out[24]:
d 6
b 7
c 3
dtype: int64
```


Another way to think about a Series is as a fixed-length, ordered dictionary, as it is a mapping of index values to data values. It can be used in many contexts where you might use a dictionary.

 Series can be converted back to a dictionary with its to_dict method:
```
In [33]: obj3.to_dict()
Out[33]: {'Ohio': 35000, 'Texas': 71000, 'Oregon': 16000, 'Utah': 5000}
```

When you are only passing a dictionary, the index in the resulting Series will respect the order of the keys according to the dictionary’s keys method, which depends on the key insertion order. You can override this by passing an index with the dictionary keys in the order you want them to appear in the resulting Series:
```
In [34]: states = ["California", "Ohio", "Oregon", "Texas"]

In [35]: obj4 = pd.Series(sdata, index=states)

In [36]: obj4
Out[36]:
California NaN
Ohio 35000.0
Oregon 16000.0
Texas 71000.0
dtype: float64
```


#### DataFrame
Represents a rectangular table of data and contains an ordered, named collection of columns, each of which can be a different value type (numeric, string, Boolean, etc.). The DataFrame has both a row and column index; it can be thought of as a dictionary of Series all sharing the same index.
```
data = {"state": ["Ohio", "Ohio", "Ohio", "Nevada", "Nevada", "Nevada"],
"year": [2000, 2001, 2002, 2001, 2002, 2003],
"pop": [1.5, 1.7, 3.6, 2.4, 2.9, 3.2]}
frame = pd.DataFrame(data)

In [50]: frame
Out[50]:
state year pop
0 Ohio 2000 1.5
1 Ohio 2001 1.7
2 Ohio 2002 3.6
3 Nevada 2001 2.4
4 Nevada 2002 2.9
5 Nevada 2003 3.2
```

For large DataFrames, the head method selects only the first five rows.

Similarly, tail returns the last five rows.

If you specify a sequence of columns, the DataFrame’s columns will be arranged in that order:
`pd.DataFrame(data, columns=["year", "state", "pop"])`

Rows can also be retrieved by position or name with the special iloc and loc attributes.


### Index objects
pandas's Index objects are responsible for holding the axis tables (including a DataFrame's column names) and other metadata (like the axis name or names). Any array or other sequence of labels you use when constructing a Series or DataFrame is Internally converted to an Index.

Immutability makes it safer to share Index objects among data structures.

| Method/Property  | Description                                                                               |
| ---------------- | ----------------------------------------------------------------------------------------- |
| `append()`       | Concatenate with additional Index objects, producing a new Index                          |
| `difference()`   | Compute set difference as an Index                                                        |
| `intersection()` | Compute set intersection                                                                  |
| `union()`        | Compute set union                                                                         |
| `isin()`         | Compute Boolean array indicating whether each value is contained in the passed collection |
| `delete()`       | Compute new Index with element at Index i deleted                                         |
| `drop()`         | Compute new Index by deleting passed values                                               |
| `insert()`       | Compute new Index by inserting element at Index i                                         |
| `is_monotonic`   | Returns True if each element is greater than or equal to the previous element             |
| `is_unique`      | Returns True if the Index has no duplicate values                                         |
| `unique()`       | Compute the array of unique values in the Index                                           |


### Essential funcionality

##### Reindexing
An important method on pandas objects is reindex, which means to create a new object with the values rearranged to align with the new index.

| Argument      | Description                                                                                                                                                  |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `labels`      | New sequence to use as an index. Can be Index instance or any other sequence-like Python data structure. An Index will be used exactly as is without any copying. |
| `index`       | Use the passed sequence as the new index labels.                                                                                                              |
| `columns`     | Use the passed sequence as the new column labels.                                                                                                            |
| `axis`        | The axis to reindex, whether "index" (rows) or "columns". The default is "index". You can alternately do `reindex(index=new_labels)` or `reindex(columns=new_labels)`. |
| `method`      | Interpolation (fill) method; "ffill" fills forward, while "bfill" fills backward.                                                                            |
| `fill_value`  | Substitute value to use when introducing missing data by reindexing. Use `fill_value="missing"` (the default behavior) when you want absent labels to have null values in the result. |
| `limit`       | When forward filling or backfilling, the maximum size gap (in number of elements) to fill.                                                                  |
| `tolerance`   | When forward filling or backfilling, the maximum size gap (in absolute numeric distance) to fill for inexact matches.                                       |
| `level`       | Match simple Index on level of MultiIndex; otherwise select subset of.                                                                                      |
| `copy`        | If True, always copy underlying data even if the new index is equivalent to the old index; if False, do not copy the data when the indexes are equivalent.   |


#### Indexing, Selection, and Filtering
Series indexing (`obj[...]`) works analogously to NumPy array indexing, except you can use the Series’s index values instead of only integers. 
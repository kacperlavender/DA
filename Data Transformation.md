### Removing Duplicates
```python
In [47]: data = pd.DataFrame({"k1": ["one", "two"] * 3 + ["two"],
    ...: ....: "k2": [1, 1, 2, 3, 3, 4, 4]})

In [48]: data
Out[48]:
    k1  k2
0  one   1
1  two   1
2  one   2
3  two   3
4  one   3
5  two   4
6  two   4

In [49]: data.duplicated()
Out[49]:
0    False
1    False
2    False
3    False
4    False
5    False
6     True
dtype: bool

In [50]: data.drop_duplicates()
Out[50]:
    k1  k2
0  one   1
1  two   1
2  one   2
3  two   3
4  one   3
5  two   4
```


### Transforming Data Using a Function or Mapping
```python
In [52]: data = pd.DataFrame({"food": ["bacon", "pulled pork", "bacon",
    ...: ....: "pastrami", "corned beef", "bacon",
    ...: ....: "pastrami", "honey ham", "nova lox"],
    ...: ....: "ounces": [4, 3, 12, 6, 7.5, 8, 3, 5, 6]})

In [53]: data
Out[53]:
          food  ounces
0        bacon     4.0
1  pulled pork     3.0
2        bacon    12.0
3     pastrami     6.0
4  corned beef     7.5
5        bacon     8.0
6     pastrami     3.0
7    honey ham     5.0
8     nova lox     6.0

In [54]: meat_to_animal = {
    ...: "bacon": "pig",
    ...: "pulled pork": "pig",
    ...: "pastrami": "cow",
    ...: "corned beef": "cow",
    ...: "honey ham": "pig",
    ...: "nova lox": "salmon"
    ...: }

In [55]: data["animal"] = data["food"].map(meat_to_animal)

In [56]: data
Out[56]:
          food  ounces  animal
0        bacon     4.0     pig
1  pulled pork     3.0     pig
2        bacon    12.0     pig
3     pastrami     6.0     cow
4  corned beef     7.5     cow
5        bacon     8.0     pig
6     pastrami     3.0     cow
7    honey ham     5.0     pig
8     nova lox     6.0  salmon
```

### Replacing Values
```python
In [57]: data = pd.Series([1., -999., 2., -999., -1000., 3.])

In [58]: data
Out[58]:
0       1.0
1    -999.0
2       2.0
3    -999.0
4   -1000.0
5       3.0
dtype: float64
```

`In [59]: data.replace(-999, np.nan)`
`In [62]: data.replace([-999,-1000], [np.nan, 0])`
`In [63]: data.replace({-999: np.nan, -1000: 0})`



### Discretization and Binning
```python
In [69]: ages = [20, 22, 25, 27, 21, 23, 37, 31, 61, 45, 41, 32]

In [70]: bins = [18, 25, 35, 60, 100]

In [71]: age_categories = pd.cut(ages, bins)

In [77]: pd.value_counts(age_categories)

Out[77]:
(18, 25]     5
(25, 35]     3
(35, 60]     3
(60, 100]    1
Name: count, dtype: int64
```

If you pass an integer number of bins to pandas.cut instead of explicit bin edges, it will compute equal-length bins based on the minimum and maximum values in the data. Consider the case of some uniformly distributed data chopped into fourths:
```python
In [81]: data = np.random.uniform(size=20)

In [82]: pd.cut(data, 4, precision=2)
Out[82]:
[(0.3, 0.53], (0.75, 0.98], (0.3, 0.53], (0.75, 0.98], (0.75, 0.98], ..., (0.75, 0.98], (0.75, 0.98], (0.3, 0.53], (0.3, 0.53], (0.3, 0.53]]
Length: 20
Categories (4, interval[float64, right]): [(0.069, 0.3] < (0.3, 0.53] < (0.53, 0.75] < (0.75, 0.98]]
```

A closely related function, pandas.qcut, bins the data based on sample quantiles. Depending on the distribution of the data, using pandas.cut will not usually result in each bin having the same number of data points. Since pandas.qcut uses sample quantiles instead, you will obtain roughly equally sized bins:
```python
In [83]: data = np.random.standard_normal(1000)

In [84]: quarilies = pd.qcut(data, 4, precision=2)

In [88]: pd.value_counts(quarilies)

Out[88]:
(-2.69, -0.72]    250
(-0.72, 0.059]    250
(0.059, 0.73]     250
(0.73, 2.99]      250
Name: count, dtype: int64
```

### Permutations
```python
In [94]: df = pd.DataFrame(np.arange(5*7).reshape((5,7)))

In [95]: df
Out[95]:
    0   1   2   3   4   5   6
0   0   1   2   3   4   5   6
1   7   8   9  10  11  12  13
2  14  15  16  17  18  19  20
3  21  22  23  24  25  26  27
4  28  29  30  31  32  33  34

In [96]: sampler = np.random.permutation(5)

In [97]: sampler
Out[97]: array([4, 1, 2, 3, 0], dtype=int32)

In [98]: df.take(sampler)
Out[98]:
    0   1   2   3   4   5   6
4  28  29  30  31  32  33  34
1   7   8   9  10  11  12  13
2  14  15  16  17  18  19  20
3  21  22  23  24  25  26  27
0   0   1   2   3   4   5   6

In [100]: column_sampler = np.random.permutation(7)

In [101]: column_sampler
Out[101]: array([6, 1, 2, 0, 3, 5, 4], dtype=int32)

In [102]: df.take(column_sampler, axis="columns")
Out[102]:
    6   1   2   0   3   5   4
0   6   1   2   0   3   5   4
1  13   8   9   7  10  12  11
2  20  15  16  14  17  19  18
3  27  22  23  21  24  26  25
4  34  29  30  28  31  33  32
```
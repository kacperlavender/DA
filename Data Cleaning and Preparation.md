During the course of doing data analysis and modeling, a significant amount of time is spent on data preparation: loading, cleaning, transforming, and rearranging. Such tasks are often reported to take up 80% or more of an analyst’s time. Sometimes the way that data is stored in files or databases is not in the right format for a particular task. Many researchers choose to do ad hoc processing of data from one form to another using a general-purpose programming language, like Python, Perl, R, or Java, or Unix text-processing tools like sed or awk. Fortunately, pandas, along with the built-in Python language features, provides you with a high-level, flexible, and fast set of tools to enable you to manipulate data into the right form.

#### Handling Missing Data
Missing data occurs commonly in many data analysis applications. One of the goals of pandas is to make working with missing data as painless as possible. For example, all of the descriptive statistics on pandas objects exclude missing data by default.

```python
In [23]: float_data = pd.Series([1.2, -3.5, np.nan, 0])

In [24]: float_data
Out[24]:
0    1.2
1   -3.5
2    NaN
3    0.0
dtype: float64

In [25]: float_data.isna()
Out[25]:
0    False
1    False
2     True
3    False
dtype: bool
```

### NA handling object methods
| Method   | Description                                                                                                                                 |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| `dropna` | Filter axis labels based on whether values for each label have missing data, with varying thresholds for how much missing data to tolerate. |
| `fillna` | Fill in missing data with some value or using an interpolation method such as "ffill" or "bfill".                                           |
| `isna`   | Return Boolean values indicating which values are missing/NA.                                                                               |
| `notna`  | Negation of `isna`, returns `True` for non-NA values and `False` for NA values.                                                             |


### Filtering Out Missing Data
```python
In [30]: data = pd.Series([1, np.nan, 3.5, np.nan, 7])

In [31]: data.dropna()
Out[31]:
0    1.0
2    3.5
4    7.0
dtype: float64

# same thing as:
In [32]: data[data.notna()]
Out[32]:
0    1.0
2    3.5
4    7.0
dtype: float64
```


With DataFrame objects, there are different ways to remove missing data. You may want to drop rows or columns that are all NA, or only those rows or columns containing any NAs at all. dropna by default drops any row containing a missing value:
```python
In [33]: data = pd.DataFrame([[1., 6.5, 3.], [1., np.nan, np.nan],
    ...: ....: [np.nan, np.nan, np.nan], [np.nan, 6.5, 3.]])

In [34]: data
Out[34]:
     0    1    2
0  1.0  6.5  3.0
1  1.0  NaN  NaN
2  NaN  NaN  NaN
3  NaN  6.5  3.0

In [35]: data.dropna()
Out[35]:
     0    1    2
0  1.0  6.5  3.0

In [36]: data.dropna(how="all")
Out[36]:
     0    1    2
0  1.0  6.5  3.0
1  1.0  NaN  NaN
3  NaN  6.5  3.0
```
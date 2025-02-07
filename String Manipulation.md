pandas extension data types

| Extension type    | Description |
|-------------------|-------------|
| **BooleanDtype**  | Nullable Boolean data, use `"boolean"` when passing as string |
| **CategoricalDtype** | Categorical data type, use `"category"` when passing as string |
| **DatetimeTZDtype** | Datetime with time zone |
| **Float32Dtype** | 32-bit nullable floating point, use `"Float32"` when passing as string |
| **Float64Dtype** | 64-bit nullable floating point, use `"Float64"` when passing as string |
| **Int8Dtype** | 8-bit nullable signed integer, use `"Int8"` when passing as string |
| **Int16Dtype** | 16-bit nullable signed integer, use `"Int16"` when passing as string |
| **Int32Dtype** | 32-bit nullable signed integer, use `"Int32"` when passing as string |
| **Int64Dtype** | 64-bit nullable signed integer, use `"Int64"` when passing as string |
| **UInt8Dtype** | 8-bit nullable unsigned integer, use `"UInt8"` when passing as string |
| **UInt16Dtype** | 16-bit nullable unsigned integer, use `"UInt16"` when passing as string |
| **UInt32Dtype** | 32-bit nullable unsigned integer, use `"UInt32"` when passing as string |
| **UInt64Dtype** | 64-bit nullable unsigned integer, use `"UInt64"` when passing as string |

### Python Built-In String Objects Methods
```python
In [46]: val = "a, b, guido"

In [47]: val.split(",")
Out[47]: ['a', ' b', ' guido']
```

split is often combined with strip to trim whitespace (including line breaks):
```python
In [48]: pieces = [x.strip() for x in val.split(",")]

In [49]: pieces
Out[49]: ['a', 'b', 'guido']
```

#### Python built-in string methods
| Method      | Description |
|------------|-------------|
| **count**  | Return the number of nonoverlapping occurrences of substring in the string |
| **endswith** | Return True if string ends with suffix |
| **startswith** | Return True if string starts with prefix |
| **join** | Use string as delimiter for concatenating a sequence of other strings |
| **index** | Return starting index of the first occurrence of passed substring if found in the string; otherwise, raises ValueError if not found |
| **find** | Return position of first character of first occurrence of substring in the string; like index, but returns –1 if not found |
| **rfind** | Return position of first character of last occurrence of substring in the string; returns –1 if not found |
| **replace** | Replace occurrences of string with another string |
| **strip**, **rstrip**, **lstrip** | Trim whitespace, including newlines on both sides, on the right side, or on the left side, respectively |
| **split** | Break string into list of substrings using passed delimiter |
| **lower** | Convert alphabet characters to lowercase |
| **upper** | Convert alphabet characters to uppercase |
| **casefold** | Convert characters to lowercase, and convert any region-specific variable character combinations to a common comparable form |
| **ljust**, **rjust** | Left justify or right justify, respectively; pad opposite side of string with spaces (or some other fill character) to return a string with a minimum width |


### Partial listing of Series string methods
| Method      | Description |
|------------|-------------|
| **cat** | Concatenate strings element-wise with optional delimiter |
| **contains** | Return Boolean array if each string contains pattern/regex |
| **count** | Count occurrences of pattern |
| **extract** | Use a regular expression with groups to extract one or more strings from a Series of strings; the result will be a DataFrame with one column per group |
| **endswith** | Equivalent to x.endswith(pattern) for each element |
| **startswith** | Equivalent to x.startswith(pattern) for each element |
| **findall** | Compute list of all occurrences of pattern/regex for each string |
| **get** | Index into each element (retrieve i-th element) |
| **isalnum** | Equivalent to built-in str.alnum |
| **isalpha** | Equivalent to built-in str.isalpha |
| **isdecimal** | Equivalent to built-in str.isdecimal |
| **isdigit** | Equivalent to built-in str.isdigit |
| **islower** | Equivalent to built-in str.islower |
| **isnumeric** | Equivalent to built-in str.isnumeric |
| **isupper** | Equivalent to built-in str.isupper |
| **join** | Join strings in each element of the Series with passed separator |
| **len** | Compute length of each string |
| **lower**, **upper** | Convert cases; equivalent to x.lower() or x.upper() for each element |
| **match** | Use re.match with the passed regular expression on each element, returning True or False whether it matches |
| **pad** | Add whitespace to left, right, or both sides of strings |
| **center** | Equivalent to pad(side="both") |
| **repeat** | Duplicate values (e.g., s.str.repeat(3) is equivalent to x * 3 for each string) |
| **replace** | Replace occurrences of pattern/regex with some other string |
| **slice** | Slice each string in the Series |
| **split** | Split strings on delimiter or regular expression |
| **strip** | Trim whitespace from both sides, including newlines |
| **rstrip** | Trim whitespace on right side |
| **lstrip** | Trim whitespace on left side |


### Categorical Data
This section introduces the pandas Categorical type. I will show how you can achieve better performance and memory use in some pandas operations by using it. I also introduce some tools that may help with using categorical data in statistics and machine learning applications

Frequently, a column in a table may contain repeated instances of a smaller set of distinct values. We have already seen functions like unique and value_counts, which enable us to extract the distinct values from an array and compute their frequencies, respectively:

Categorical methods for Series in pandas

| Method                       | Description                                                                                         |
| ---------------------------- | --------------------------------------------------------------------------------------------------- |
| **add_categories**           | Append new (unused) categories at end of existing categories                                        |
| **as_ordered**               | Make categories ordered                                                                             |
| **as_unordered**             | Make categories unordered                                                                           |
| **remove_categories**        | Remove categories, setting any removed values to null                                               |
| **remove_unused_categories** | Remove any category values that do not appear in the data                                           |
| **rename_categories**        | Replace categories with indicated set of new category names; cannot change the number of categories |
| **reorder_categories**       | Behaves like rename_categories, but can also change the result to have ordered categories           |
| **set_categories**           | Replace the categories with the indicated set of new categories; can add or remove categories       |

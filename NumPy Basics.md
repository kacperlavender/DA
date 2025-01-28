Here are some of the things you will find in NumPy:
- darray, an efficient multidimensional array providing fast array-oriented arithmetic operations and flexible broadcasting capabilities
- Mathematical functions for fast operations on entire arrays of data without having to write loops
- Tools for reading/writing array data to disk and working with memory-mapped files
- Linear algebra, random number generation, and Fourier transform capabilities
- A C API for connecting NumPy with libraries written in C, C++, or FORTRAN

### Array object
One of the key features of NumPy is its N-dimensional array object, or ndarray, which is a fast, flexible container for large datasets in Python. Arrays enable you to perform mathematical operations on whole blocks of data using similar syntax to the equivalent operations between scalar elements.

#### Creating ndarrays
The easiest way to create an array is to use the array function. This accepts any sequence-like object (including other arrays) and produces a new NumPy array containing the passed data. For example:
```
In [19]: data1 = [6, 7.5, 8, 0, 1]

In [20]: arr1 = np.array(data1)

In [21]: arr1
Out[21]: array([6. , 7.5, 8. , 0. , 1. ])
```
 or two dimensional: 
```
In [22]: data2 = [[1, 2, 3, 4], [5, 6, 7, 8]]

In [23]: arr2 = np.array(data2)

In [24]: arr2
Out[24]:
array([[1, 2, 3, 4],
       [5, 6, 7, 8]]) 
```


`numpy.arange` is an array-valued version of the built-in Python range function:
```
In [32]: np.arange(15)
Out[32]: array([ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14])
```


| Function             | Description                                                                                                    |
|----------------------|----------------------------------------------------------------------------------------------------------------|
| `array`             | Convert input data (list, tuple, array, or other sequence type) to an `ndarray` either by inferring a data type or explicitly specifying a data type; copies the input data by default |
| `asarray`           | Convert input to `ndarray`, but do not copy if the input is already an `ndarray`                               |
| `arange`            | Like the built-in `range` but returns an `ndarray` instead of a list                                           |
| `ones`, `ones_like` | Produce an array of all 1s with the given shape and data type; `ones_like` takes another array and produces a ones array of the same shape and data type |
| `zeros`, `zeros_like` | Like `ones` and `ones_like` but producing arrays of 0s instead                                               |
| `empty`, `empty_like` | Create new arrays by allocating new memory, but do not populate with any values like `ones` and `zeros`       |
| `full`, `full_like` | Produce an array of the given shape and data type with all values set to the indicated “fill value”; `full_like` takes another array and produces a filled array of the same shape and data type |
| `eye`, `identity`   | Create a square N × N identity matrix (1s on the diagonal and 0s elsewhere)                                    |


#### Arithmetic with NumPy Arrays
Arrays are important because they enable you to express batch operations on data without writing any for loops. NumPy users call this vectorization. Any arithmetic operations between equal-size arrays apply the operation element-wise.


#### Basic Indexing and Slicing
NumPy array indexing is a deep topic, as there are many ways you may want to select a subset of your data or individual elements. One-dimensional arrays are simple; on the surface they act similarly to Python lists:
```
In [61]: arr = np.arange(10)

In [62]: arr
Out[62]: array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])

In [63]: arr[5]
Out[63]: 5

In [64]: arr[5:8]
Out[64]: array([5, 6, 7])
```

With higher dimensional arrays, you have many more options. In a two-dimensional
array, the elements at each index are no longer scalars but rather one-dimensional
arrays:
```
In [73]: arr2d = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])

In [74]: arr2d[2]
Out[74]: array([7, 8, 9])
```
Thus, individual elements can be accessed recursively:
```
In [75]: arr2d[0][2]
Out[75]: 3

In [76]: arr2d[0, 2]
Out[76]: 3
```


### Transposing Arrays and Swapping Axes
Transposing is a special form of reshaping that similarly returns a view on the underlying data without copying anything. Arrays have the transpose method and the special T attribute:
```
In [132]: arr = np.arange(15).reshape((3, 5))

In [133]: arr
Out[133]:
array([[ 0, 1, 2, 3, 4],
[ 5, 6, 7, 8, 9],
[10, 11, 12, 13, 14]])

In [134]: arr.T
Out[134]:
array([[ 0, 5, 10],
[ 1, 6, 11],
[ 2, 7, 12],
[ 3, 8, 13],
[ 4, 9, 14]])
```

```
arr = np.array([[0, 1, 0], [1, 2, -2], [6, 3, 2], [-1, 0, -1], [1, 0, 1]])

np.dot(arr.T, arr) # multiplation of arr^T and arr

# another way to do it is with @:
arr.T @ arr
array([[39, 20, 12],
       [20, 14,  2],
       [12,  2, 10]])

```
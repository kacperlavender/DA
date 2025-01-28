#### Data Structures and Sequences
##### Tuple 
A *tuple* is a fixed-length, immutable sequence od Python objects which, once assigned, cannot be changed.

```
In [32]: seq = [(1, 2, 3), (4, 5, 6), (7, 8, 9)]
In [33]: for a, b, c in seq:
....: print(f'a={a}, b={b}, c={c}')
a=1, b=2, c=3
a=4, b=5, c=6
a=7, b=8, c=9
```

```
In [34]: values = 1, 2, 3, 4, 5
In [35]: a, b, *rest = values
In [36]: a
Out[36]: 1
In [37]: b
Out[37]: 2
In [38]: rest
Out[38]: [3, 4, 5]
```


##### List
In contrast with tuples, lists are variable length and their contents can be modified in place. Lists are mutable.

###### Adding and removing elements
Elements can be appended to the end of the list with the append method:
```
In [51]: b_list.append("dwarf")
In [52]: b_list
Out[52]: ['foo', 'peekaboo', 'baz', 'dwarf']
```

Using insert you can insert an element at a specific location in the list:
```
In [53]: b_list.insert(1, "red")
In [54]: b_list
Out[54]: ['foo', 'red', 'peekaboo', 'baz', 'dwarf']
```
The insertion index must be between 0 and the length of the list, inclusive.


###### Sorting
You can sort a list in place (without creating a new object) by calling its function:
```
In [67]: a = [7, 2, 5, 1, 3]
In [68]: a.sort()
In [69]: a
Out[69]: [1, 2, 3, 5, 7]
```

Sorting by `len`
```
In [70]: b = ["saw", "small", "He", "foxes", "six"]
In [71]: b.sort(key=len)
In [72]: b
Out[72]: ['He', 'saw', 'six', 'small', 'foxes']
```


##### Dictionary
A dictionary stores a collection of key-value pairs, where key and value are Python objects. Each key is associated with a value so that a value can be conveniently retrieved, inserted, modified, or deleted given a particular key.
```
In [83]: empty_dict = {}
In [84]: d1 = {"a": "some value", "b": [1, 2, 3, 4]}
In [85]: d1
Out[85]: {'a': 'some value', 'b': [1, 2, 3, 4]}
```

You can delete values using either the del keyword of the pop method (which simultaneously returns the value and deletes the key):

The keys and values method gives you iterators of the dictionary’s keys and values, respectively. The order of the keys depends on the order of their insertion, and these functions output the keys and values in the same respective order. f you need to iterate over both the keys and values, you can use the items method to iterate over the keys and values as 2-tuples.


With setting values, it may be that the values in a dictionary are another kind of collection, like a list. For example, you could imagine categorizing a list of words by their first letters as a dictionary of lists:
```
words = ['apple', 'bat', 'bar', 'atom', 'book']
by_letter = {}

for word in words:
    letter = word[0]
    if letter not in by_letter:
        by_letter[letter] = [word]
    else:
        by_letter[letter].append(word)

by_letter

{'a': ['apple', 'atom'], 'b': ['bat', 'bar', 'book']}
```



##### Set
A `set` is an unordered collection of unique elements.

| Function                           | Alternative | Description                                                            |
| ---------------------------------- | ----------- | ---------------------------------------------------------------------- |
| `a.add(x)`                         | N/A         | Add element `x` to set `a`                                             |
| `a.clear()`                        | N/A         | Reset set `a` to an empty state, discarding all of its elements        |
| `a.remove(x)`                      | N/A         | Remove element `x` from set `a`                                        |
| `a.pop()`                          | N/A         | Remove an arbitrary element from set `a`, raising KeyError if empty    |
| `a.union(b)`                       | `a          | All of the unique elements in `a` and `b`                              |
| `a.update(b)`                      | `a          | Set the contents of `a` to be the union of the elements in `a` and `b` |
| `a.intersection(b)`                | `a & b`     | All of the elements in both `a` and `b`                                |
| `a.intersection_update(b)`         | `a &= b`    | Set the contents of `a` to be the intersection of `a` and `b`          |
| `a.difference(b)`                  | `a - b`     | The elements in `a` that are not in `b`                                |
| `a.difference_update(b)`           | `a -= b`    | Set `a` to the elements in `a` that are not in `b`                     |
| `a.symmetric_difference(b)`        | `a ^ b`     | All of the elements in either `a` or `b` but not both                  |
| `a.symmetric_difference_update(b)` | `a ^= b`    | Set `a` to contain the elements in either `a` or `b` but not both      |
| `a.issubset(b)`                    | `<=`        | True if the elements of `a` are all contained in `b`                   |
| `a.issuperset(b)`                  | `>=`        | True if the elements of `b` are all contained in `a`                   |
| `a.isdisjoint(b)`                  | N/A         | True if `a` and `b` have no elements in common                         |


#### enumerate
It’s common when iterating over a sequence to want to keep track of the index of the current item.
Instead of:
```
index = 0
for value in collection:
# do something with value
index += 1
```
You can do:
```
for index, value in enumerate(collection):
# do something with value
```


##### sorted
The sorted function returns a new sorted list from the elements of any sequence:
```
In [145]: sorted([7, 1, 2, 6, 0, 3, 2])
Out[145]: [0, 1, 2, 2, 3, 6, 7]

In [146]: sorted("horse race")
Out[146]: [' ', 'a', 'c', 'e', 'e', 'h', 'o', 'r', 'r', 's']
```


#### List, Set, and Dictionary Comprehensions
`[expr for value in collection if condition]`
is equivalent to:
```
result = []
for value in collection:
	if condition:
	result.append(expr)
```

A dictionary comprehension looks like this:
```
dict_comp = {key-expr: value-expr for value in collection if condition}
```


As a simple dictionary comprehension example, we could create a lookup map of these strings for their locations in the list:
```
In [160]: loc_mapping = {value: index for index, value in enumerate(strings)}

In [161]: loc_mapping
Out[161]: {'a': 0, 'as': 1, 'bat': 2, 'car': 3, 'dove': 4, 'python': 5}
```


### Files and Operating System
`In [234]: f = open(path, encoding="utf-8")`

| Mode | Description                                                                                         |
| ---- | --------------------------------------------------------------------------------------------------- |
| `r`  | Read-only mode                                                                                      |
| `w`  | Write-only mode; creates a new file (erasing the data for any file with the same name)              |
| `x`  | Write-only mode; creates a new file but fails if the file path already exists                       |
| `a`  | Append to existing file (creates the file if it does not already exist)                             |
| `r+` | Read and write                                                                                      |
| `b`  | Add to mode for binary files (e.g., `"rb"` or `"wb"`)                                               |
| `t`  | Text mode for files (automatically decoding bytes to Unicode); this is the default if not specified |

```
In [235]: lines = [x.rstrip() for x in open(path, encoding="utf-8")]

In [236]: lines
Out[236]:
 ['Sueña el rico en su riqueza,',
 'que más cuidados le ofrece;',
 '',
 'sueña el pobre que padece',
 'su miseria y su pobreza;',
 '',
 'sueña el que a medrar empieza,',
 'sueña el que afana y pretende,',
 'sueña el que agravia y ofende,',
 '',
 'y en el mundo, en conclusión,',
 'todos sueñan lo que son,',
 'aunque ninguno lo entiende.',
 '']
```

When you use open to create file objects, it is recommended to close the file when you are finished with it. Closing the file releases its resources back to the operating system:
`In [237]: f.close()`

| Method/Attribute         | Description                                                                                       |
|--------------------------|---------------------------------------------------------------------------------------------------|
| `read([size])`           | Return data from the file as bytes or string depending on the file mode, with an optional `size` argument indicating the number of bytes or string characters to read |
| `readable()`             | Return `True` if the file supports read operations                                               |
| `readlines([size])`      | Return a list of lines in the file, with an optional `size` argument                             |
| `write(string)`          | Write the passed string to the file                                                              |
| `writable()`             | Return `True` if the file supports write operations                                              |
| `writelines(strings)`    | Write the passed sequence of strings to the file                                                 |
| `close()`                | Close the file object                                                                            |
| `flush()`                | Flush the internal I/O buffer to disk                                                            |
| `seek(pos)`              | Move to the indicated file position (integer)                                                   |
| `seekable()`             | Return `True` if the file object supports seeking and thus random access (some file-like objects do not) |
| `tell()`                 | Return the current file position as an integer                                                   |
| `closed`                 | `True` if the file is closed                                                                     |
| `encoding`               | The encoding used to interpret bytes in the file as Unicode (typically UTF-8)                    |

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
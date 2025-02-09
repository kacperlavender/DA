Making informative visualizations (sometimes called plots) is one of the most important tasks in data analysis. It may be a part of the exploratory process—for example, to help identify outliers or needed data transformations, or as a way of generating ideas for models. For others, building an interactive visualization for the web may be the end goal. Python has many add-on libraries for making static or dynamic visualizations, but I’ll be mainly focused on matplotlib and libraries that build on top of it.

When using CMD make sure to use command
`In [22]: %matplotlib qt`


### Figures and Subplots
Plots in matplotlib reside within a Figure object. You can create a new figure with plt.figure:
```
In [26]: fig = plt.figure()

In [27]: ax1 = fig.add_subplot(2, 2, 1)

In [28]: ax2 = fig.add_subplot(2, 2, 2)

In [29]: ax3 = fig.add_subplot(2, 2, 3)

In [30]: ax3.plot(np.random.standard_normal(50).cumsum(), color="black",^M
    ...: ....: linestyle="dashed")
Out[30]: [<matplotlib.lines.Line2D at 0x1e76475fd60>]
```


To make creating a grid of subplots more convenient, matplotlib includes a plt.sub plots method that creates a new figure and returns a NumPy array containing the created subplot objects:
```python
In [39]: fig, axes = plt.subplots(2, 3)

In [40]: axes
Out[40]:
array([[<Axes: >, <Axes: >, <Axes: >],
       [<Axes: >, <Axes: >, <Axes: >]], dtype=object)

```
![[Pasted image 20250207175046.png]]


### matplotlib.pyplot.subplots options
| Argument     | Description                                                                                               |
|--------------|-----------------------------------------------------------------------------------------------------------|
| `nrows`      | Number of rows of subplots                                                                                 |
| `ncols`      | Number of columns of subplots                                                                              |
| `sharex`     | All subplots should use the same x-axis ticks (adjusting the xlim will affect all subplots)               |
| `sharey`     | All subplots should use the same y-axis ticks (adjusting the ylim will affect all subplots)               |
| `subplot_kw` | Dictionary of keywords passed to `add_subplot` call used to create each subplot                           |
| `**fig_kw`   | Additional keywords to subplots are used when creating the figure, such as `plt.subplots(2, 2, figsize=(8, 6))` |

```python
In [42]: fig, axes = plt.subplots(2,2, sharex=True, sharey=True)

In [43]: for i in range(2):
    ...:     for j in range(2):
    ...:         axes[i, j].hist(np.random.standard_normal(500), bins=50, color="black",
							     alpha=0.5)
    ...: fig.subplots_adjust(wspace=0, hspace=0)
```
![[Pasted image 20250207175442.png]]


```python
In [8]: fig = plt.figure()

In [9]: ax1 = fig.add_subplot(2,2,1)

In [10]: ax2 = fig.add_subplot(2,2,2)

In [11]: ax3 = fig.add_subplot(2,2,3)

In [12]: ax3.plot(np.random.standard_normal(50).cumsum(), color="black", linestyle="dashed")
Out[12]: [<matplotlib.lines.Line2D at 0x29205850520>]

In [13]: ax2.hist(np.random.standard_normal(100), bins=20, color="black", alpha=0.3);

In [14]: ax1.scatter(np.arange(30), np.arange(30)+ 3*np.random.standard_normal(30));
```

#### Tricks, Labels, and Legends

Setting the title, axis labels, ticks, and tick labels
```python
In [20]: fig, ax = plt.subplots()

In [21]: ax.plot(np.random.standard_normal(1000).cumsum())
Out[21]: [<matplotlib.lines.Line2D at 0x29205c44970>]

In [22]: ax.plot(np.random.standard_normal(1000).cumsum())
Out[22]: [<matplotlib.lines.Line2D at 0x292058a0040>]

In [23]: fig, ax = plt.subplots()

In [24]: ax.plot(np.random.standard_normal(1000).cumsum())
Out[24]: [<matplotlib.lines.Line2D at 0x292059008e0>]

In [25]: ticks = ax.set_xticks([0,250,500,750, 1000])

In [27]: labels = ax.set_xticklabels(["one", "two", "three", "four", "five"], rotation=30, fontsize=8)

In [28]: ax.set_xlabel("Stages")
Out[28]: Text(0.5, 14.049468184377835, 'Stages')

In [29]: ax.set_title("my first matplotlib plot")
Out[29]: Text(0.5, 1.0, 'my first matplotlib plot')

### or just
In [30]: ax.set(title="my first matplotib plot", xlabel="Stages")
Out[30]:
[Text(0.5, 1.0, 'my first matplotib plot'),
 Text(0.5, 13.939468184377828, 'Stages')]
```
![[Pasted image 20250209230953.png]]



Adding legends
```python
In [31]: fig, ax = plt.subplots()

In [32]: ax.plot(np.random.randn(1000).cumsum(), color="black", label="one");

In [33]: ax.plot(np.random.randn(1000).cumsum(), color="black",linestyle="dashed", label="two");

In [34]: ax.plot(np.random.randn(1000).cumsum(), color="black",linestyle="dotted", label="three");

In [35]: ax.legend()
Out[35]: <matplotlib.legend.Legend at 0x29208ea03d0>
```
![[Pasted image 20250209231425.png]]


Annotations and Drawings on a Subplot
```python
In [36]: fig, ax = plt.subplots()

In [37]: data = pd.read_csv("examples/spx.csv", index_col=0, parse_dates=True)

In [38]: from datetime import datetime

In [39]: spx = data["SPX"]

In [40]: spx.plot(ax=ax, color="black")
Out[40]: <Axes: xlabel='Date'>

In [41]: crisis_data = [^M
    ...:  (datetime(2007, 10, 11), "Peak of bull market"),^M
    ...:  (datetime(2008, 3, 12), "Bear Stearns Fails"),^M
    ...:  (datetime(2008, 9, 15), "Lehman Bankruptcy")^M
    ...: ]

In [42]: for date, label in crisis_data:^M
    ...:  ax.annotate(label, xy=(date, spx.asof(date) + 75),^M
    ...:  xytext=(date, spx.asof(date) + 225),^M
    ...:  arrowprops=dict(facecolor="black", headwidth=4, width=2,^M
    ...:  headlength=4),^M
    ...:  horizontalalignment="left", verticalalignment="top")
    ...:

# zoom on 2007-2010
In [43]: ax.set_xlim(["1/1/2007", "1/1/2011"])
Out[43]: (np.float64(13514.0), np.float64(14975.0))

In [44]: ax.set_ylim([600, 1800])
Out[44]: (600.0, 1800.0)

In [45]: ax.set_title("Important dates in the 2008-2009 financial crisis")
Out[45]: Text(0.5, 1.0, 'Important dates in the 2008-2009 financial crisis')
```
![[Pasted image 20250209231908.png]]

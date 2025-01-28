### Numpy
Short for Numerical Python, as long been a cornerstone of numerical computing in Python. It provides the data structures, algorithms, and library glue needed for most scientific applications involving numerical data in Python. NumPy contains, among other things:
1. A fast and efficient multidimensional array object `ndarray`
2. Functions for performing element-wise computations with arrays or mathematical operations between arrays
3. Tools for reading and writing array-based datasets to disk
4. Linear algebra operations, Fourier transform, and random number generation
5.  A mature C API to enable Python extensions and native C or C++ code to access NumPy’s data structures and computational facilities

### pandas
Pandas is a powerful Python library for working with structured or tabular data, providing intuitive and flexible tools for data manipulation and analysis. It was created in 2008 and has since become a cornerstone of Python's data analysis ecosystem. The name "pandas" derives from **panel data** (multidimensional structured datasets) and reflects its focus on Python-based data analysis.

- **Core Data Structures**: 
  - `DataFrame`: A tabular, column-oriented data structure with row and column labels.
  - `Series`: A one-dimensional labeled array.
- **Data Manipulation**: Tools for reshaping, slicing, aggregating, and selecting subsets of data.
- **Time Series Support**: Integrated functionality for handling time-indexed data.
- **Missing Data Handling**: Flexible methods to manage incomplete datasets.
- **Relational Operations**: Merge and join functionality similar to SQL databases.

Pandas combines the array-computing power of NumPy with data manipulation capabilities found in spreadsheets and relational databases. It was originally built to solve finance and business analytics problems, making it particularly strong in handling time-series data.


### matplotlib
the most popular Python library for producing plots and other two-dimensional data visualizations. It was originally created by John D. Hunter and is now maintained by a large team of developers. It is designed for creating plots suitable for publication. While there are other visualization libraries available to Python programmers, matplotlib is still widely used and integrates reasonably well with the rest of the ecosystem. I think it is a safe choice as a default visualization tool.

### IPython and Jupyter
While it does not provide any computational or data analytical tools by itself, IPython is designed for both interactive computing and software development work. It encourages an execute-explore workflow instead of the typical edit-compile-run workflow of many other programming languages. It also provides integrated access to your operating system’s shell and filesystem; this reduces the need to switch between a terminal window and a Python session in many cases.


### SciPy
A collection of packages addressing a number of foundational problems in scientific computing.\


### scikit-learn
become the premier general purpose machine learning toolkit for Python programmers. As of this writing, more than two thousand different individuals have contributed code to the project


### statsmodels
Compared with scikit-learn, statsmodels contains algorithms for classical (primarily frequentist) statistics and econometrics. This includes such submodules as: 
1. Regression models: linear regression, generalized linear models, robust linear models, linear mixed effects models, etc.
2. Analysis of variance (ANOVA)
3. Time series analysis: AR, ARMA, ARIMA, VAR, and other models
4. Nonparametric methods: Kernel density estimation, kernel regression
5. Visualization of statistical model results
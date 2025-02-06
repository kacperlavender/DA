#### Text and binary data loading functions in pandas
| Function          | Description |
|------------------|----------------------------------------------------------------|
| `read_csv`       | Load delimited data from a file, URL, or file-like object; uses comma as the default delimiter. |
| `read_fwf`       | Read data in fixed-width column format (i.e., no delimiters). |
| `read_clipboard` | Variation of `read_csv` that reads data from the clipboard; useful for converting tables from web pages. |
| `read_excel`     | Read tabular data from an Excel XLS or XLSX file. |
| `read_hdf`       | Read HDF5 files written by pandas. |
| `read_html`      | Read all tables found in the given HTML document. |
| `read_json`      | Read data from a JSON string, file, URL, or file-like object. |
| `read_feather`   | Read the Feather binary file format. |
| `read_orc`       | Read the Apache ORC binary file format. |
| `read_parquet`   | Read the Apache Parquet binary file format. |
| `read_pickle`    | Read an object stored by pandas using the Python pickle format. |
| `read_sas`       | Read a SAS dataset stored in one of SAS system’s custom storage formats. |
| `read_spss`      | Read a data file created by SPSS. |
| `read_sql`       | Read the results of a SQL query (using SQLAlchemy). |
| `read_sql_table` | Read a whole SQL table (using SQLAlchemy); equivalent to selecting everything using `read_sql`. |
| `read_stata`     | Read a dataset from Stata file format. |
| `read_xml`       | Read a table of data from an XML file. |

Overview of the mechanics of these functions, which are meant to convert text data into a DataFrame. The optional arguments for these functions may fall into a few categories:
Indexing
	Can treat one or more columns as the returned DataFrame, and whether to get column names from the file, arguments you provide, or not at all.
Type inference and data conversion
	Includes the user-defined value conversions and custom list of missing value markers.
Date and time parsing
	Includes a combining capability, including combining date and time information spread over multiple columns into a single column in the result.
Iterating
	Support for iterating over chunks of very large files.
Unclean data issues
	Includes skipping rows or a footer, comments, or other minor things like numeric data with thousands separated by commas
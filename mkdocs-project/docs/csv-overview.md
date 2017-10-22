# Learn CSV / CSV Overview #

Comma-separated-value (CSV) files are perhaps the simplest format that can be used for a dataset.
It is for this reason that CSV files are generally supported by many tools, including spreadsheets,
database import/export, open data portals, geographic information systems, visualization tools, and other software tools.
The basic syntax of a CSV file is columns of data separated by a comma.
An alternate delimiter character can be used.  For example, using a tab character as delimiter would result in tab-delimited-file.
The pipe or vertical bar (`|`) is another common delimiter.
An example CSV file, with heading and data rows is as follows:

```text
"column1","column2","column3"
text one,123,123.0
text two,234,234.0
text three,345,345.0
```

CSV files may be used as the master copy of a dataset or a data exchange format created from a master copy.
In both cases, dealing with the limitations of CSV is critical to ensuring data integrity.

The [CSV Syntax documentation](csv-syntax) describes syntax and limitations.

## CSV Benefits ##

* Very simple format that can be handled by many software programs
* File size is generally small because the file mainly consists of data values and often compresses well

## CSV Limitations ##

* No native metadata format and therefore requires assumptions or implementation-specific approach
* Can be difficult to view/edit in a text editor due to lack of formatting
* Errors in formatting (such as commas used in data) can be difficult to detect due to simple format

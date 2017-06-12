# OWF Learn CSV / CSV Syntax

CSV file syntax is, on the surface, relatively basic.
However, there are a number of considerations that must be handled in software.
Because the CSV format is not a universal standard,
the topics described below must be understood from the standpoint of
CSV-producing and CSV-consuming software.

This page contains the following sections:

* [Syntax Overview](#syntax-overview)
	+ [Comments](#comments)
	+ [Column Headers](#column-headers)
	+ [Data Rows](#data-rows)
	+ [Data Values in Row](#data-values-in-row)
* [CSV Syntax Topics](#csv-syntax-topics)
	+ [Metadata and Schema](#metadata-and-schema)
	+ [Data Types](#data-types)
	+ [Missing Values](#missing-values)
	+ [End of Line](#end-of-line)
	+ [Versioning](#versioning)
	+ [CSV as Web Service Resource](#csv-as-web-service-resource)

## Syntax Overview

CSV files typically consist of rows/columns of data consistent with a data table,
where columns are separated by a comma, and lines are separated by end of line.
Within a CSV file may exist the following:

* [Comments](#comments)
* [Column Headers](#column-headers) - see also [Metadata and Schema](#metadata-and-schema)
* [Data Rows](#data-rows)
* [Data Values in Row](#data-values-in-row)

A simple example illustrating the above components is as shown below:

```text
# Comment1
# Comment2
"column1","column2","column3"
text one,123,123.0
text two,234,234.0
text three,345,345.0
```

### Comments

CSV files do not have a standard comment syntax.
However, the following comment strategies are often used:

* Use `#` character as the first character in the line.
* **TODO smalers 2017-06-12 need to investigate other options and reference tools.**


### Column Headers

Column headers (or headings) may be optional or required.
If used, the headers are typically the first non-comment row and conform to the following:

* May or may not require/support being surrounded by double or single quotes.
Using quotes can indicate that the row does contain header information.
* May or may not use conventions such as specifying column data units in parentheses.
* Applications that produce and consume CSV files must be consistent when handling column headers.
For example, consuming code may search for a case-independent match of a column header,
or a part of the header, to ensure a unique match.

### Data Rows

CSV data rows are delineated by end of line character(s).
Because CSV files are text files, the end of line may adhere to the operating system preference,
which is linefeed `LF` (newline) on Linux and Mac, carriage-return and linefeed `CRLF` on Windows.

The last line in the file may or may not contain an end of line (may just contain end of file).

### Data Values in Row

The data values in a row are consistent with the column and may also be referred to as "cell values".
The following characteristics for values apply:

* Typically should not have surrounding whitespace (space),
and consuming software can trim such characters to be safe
* Data type is typically consistent within a column because software applications typically map the
data values to data objects of a specific type.
* Data format is typically consistent with the data type and data units.
In particular, floating point numbers will use a number of digits after the decimal point (precision)
suitable for the data units.
Although floating point numbers may use commas to separate thousand multipliers, raw data CSV files
typically omit such formatting because it complicates reading the data because the
commas used in formatting the values conflict with the comma delimiter.
* Text (strings) that contain comma are typically surrounded by double or single quotes to ensure
that the internal comma is not confused with the delimiter character.
* See discussion of [missing data](#missing-values).

## CSV Syntax Topics

The following sections discuss specific topics that are relevant to CSV files.

### Metadata and Schema

A limitation of CSV files is that the file syntax does not by default support metadata and schema specification.
Metadata in generic terms is information about the data, such as longer description, data units, source, quality, etc.
A schema is a specific format that can be processed by software to understand the file format,
for example, to provide data integration and validation features.
A lack of metadata and schema may not be an issue because the file format is simple.
However, such information can help document the data and facilitate use and integration.

There is not currently a universal standard for metadata.
However, the following are emerging standards that may be useful:

* [Frictionless Data Specification](https://specs.frictionlessdata.io/table-schema/) - JSON schema file to accompany the CSV file
* **TODO smalers 2017-06-12 need to research other options including from [above's related work](https://specs.frictionlessdata.io/table-schema/#appendix:-related-work).**

One issue is that if using a CSV format as a web service, then the schema must be retrieved as a second request.

### Data Types

Data types in CSV files may or may not be handled intelligently by producing and consuming software.
The following considerations are important:

* Text (string)
	- may or may not be surrounded by single or double quotes
	- if contain comma(s), will be surrounded by single or double quotes
	- may or may not contain embedded end of lines, if included may break consuming software
	- blank value indicates empty string
* Integer number
	- generally simple to handle but producing or consuming software may treat integers and floating point numbers the same
	- missing values may be indicated by blank value or a special value (such as `null`) that must be interpreted
* Floating point number
	- generally simple to handle but producing or consuming software may treat integers and floating point numbers the same
	- missing values may be indicated by blank value or a special value (such as `null` or `NaN`) that must be interpreted
* Boolean
	- generally simple to handle but producing or consuming software may treat as integer
	- may or may not support `0`, `1`, `false`, `true`, `no`, `yes`, depending on software
	- missing values may be indicated by blank value or a special value (such as `null` or `NaN`) that must be interpreted
* Date/time
	- Can be difficult to deal with because of various formatting standards, time zone, daylight savings, etc.
	- Often handled as a string that requires parsing to read
	- [ISO 8601 specification](https://en.wikipedia.org/wiki/ISO_8601) is helpful to ensure standardization

### Missing Values

Missing values may be indicated in a number of ways as per the [Data Types section](#data-types).
One of the bigger issues is whether a string value of `null` or `"null"` is converted to the proper data object type
(see constraints of the specific tool).

### End of Line

As indicated previously, the CSV end of line is typically consistent with the operating system for the computer that generated the file,
but is not necessarily so.  For example, the simpler Linux style may be used in all cases.
Typically text editors and software that read CSV files should gracefully handle the variations of end of line:

* Linux, Mac - line feed, `LF`
* Windows - carriage return and line feed, `CRLF`

### Versioning

Because CSV files are text files, they can be easily versioned.
A corresponding schema, which is saved as a text file, can also be versioned. 

### CSV as Web Service Resource

CSV files are often used with web services and have the mime type `text/csv` as per [RFC 4180](https://tools.ietf.org/html/rfc4180).
However, experience has shown that this may not work with some applications.  The Mozilla list provides a reference:

* [Complete list of MIME types](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types/Complete_list_of_MIME_types)

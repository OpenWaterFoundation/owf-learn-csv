# Learn CSV / CSV with TSTool #

The TSTool software automates processing of time series, tabular, and other data.
For example, TSTool can read a table from an Excel worksheet and output the table to a CSV file,
with control over data types and formatting.
Information about TSTool can be found at the following page:

* [TSTool software at the Open Water Foundation](http://openwaterfoundation.org/software-tools/tstool) 

## TSTool Commands for CSV Processing ##

TSTool provides several commands for processing CSV data, including reading from various tabular formats
and writing to CSV.  See the command reference documentation for the software and the following
tests, which illustrate usage:

* [ReadDelimitedFile](https://github.com/OpenWaterFoundation/cdss-app-tstool-test/tree/master/test/regression/commands/general/ReadDelimitedFile) - read time series from CSV
* [WriteDelimitedFile](https://github.com/OpenWaterFoundation/cdss-app-tstool-test/tree/master/test/regression/commands/general/WriteDelimitedFile) - write time series to CSV
* [ReadTableFromDelimitedFile](https://github.com/OpenWaterFoundation/cdss-app-tstool-test/tree/master/test/regression/commands/general/ReadTableFromDelimitedFile) - read table from CSV
* [WriteTableToDelimitedFile](https://github.com/OpenWaterFoundation/cdss-app-tstool-test/tree/master/test/regression/commands/general/WriteTableToDelimitedFile) - write table to CSV

## TSTool Examples ##

The Open Water Foundation uses TSTool to automate processing datasets maintained in Excel
into CSV files.  For example, the following datasets maintained in GitHub use a `data` (or similar) folder for
Excel input and CSV output, with the TSTool command files in the `analysis` (or similar) folder.
Files with extension `.TSTool` or `.tstool` can be opened and run in TSTool to process data:

* [Colorado Municipalities](https://github.com/OpenWaterFoundation/owf-data-co-municipalities)
* [Main OWF data page](http://data.openwaterfoundation.org/) - follow links to datasets

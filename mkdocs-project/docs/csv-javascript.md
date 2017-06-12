# OWF Learn CSV / CSV for JavaScript

This page provides information about using CSV format with JavaScript.

The following sections are available in this documentation:

* [JavaScript Language](#javascript-language) - reading and writing directly using JavaScript language
* [Papa Parse](#papa-parse) - a useful library

## JavaScript Language

**TODO smalers 2017-06-12 need to describe example of how to create and parse CSV using core JavaScript.
No need to provide complete solution but point out basics that illustrate why a library is helpful.**

## Papa Parse

Papa Parse is a fast and powerful, in-browser CSV (delimeted text) parser that gracefully handles large files and malformed input. 

Click here for more information on [Papa Parse](http://papaparse.com)

* [Convert CSV to JSON](#convert-csv-to-json)
	* [Parse String](#parse-string)
	* [Parse local file](#parse-local-file)
	* [Parse remote file](#parse-remote-file)
	* [Using jQuery to select files](#using-jquery-to-select-files)
* [Convert JSON to CSV](#convert-json-to-csv)
* [Config](#config)
* [Results](#results)
	* [Data](#data)
	* [Errors](#errors)
	* [Meta](#meta)
* [Extras](#extras)

### Convert CSV to JSON

Delimeted data can be parsed out of strings or files using PapaParse. Files that are parsed can be parsed either locally or remotely. This type of conversion will take a CSV file and convert it into a JSON object that contains the following properties:

* data
* errors
* meta 

#### Parse String
```
Papa.parse(csvString[, config])
```

* **csvString** is a string delimited text to be parsed.
* **config** is an optional config object

**Example:**

```
var parsed_string = Papa.parse("column1, column2, column3\n123,456,789");
console.log(parsed_string);
```

#### Parse Local File

```
Papa.parse(file, config);
```
* **file** is a File object obtained from the DOM (Document Object Model).

```
Papa.parse(file, {
	complete: function(result){
		console.log(result);
	}
});
```
In this example above, the results are provided in the **complete** callback function. 

#### Parse Remote File

```
Papa.parse(url, {
	download: true,
	// other configure options
});
```

* **url** is the path or URL to the file being downloaded.
* The second argument is a **config object** where **download: true** is set.
* The code above does not actually return anything. The results are provided asynchronously to a callback function.

**Example:**

```
```


#### Using jQuery to Select Files

```
```

### Convert JSON to CSV

```
$.get(file, function(result){
	var parsed_file = Papa.parse(result);
	console.log(parsed_file);
});
```
* **url** or **file path** to the file being parsed.
* **result** is the data being passed to PapaParse

**Example:**
```
$.get("test-data.csv",function(result){
	var parsed_file = Papa.parse(result);
	console.log(parsed_file);
});

```

### Config

```
```

### Results

```
```

#### Data

An array of rows. If the header option specified in the config object is false, rows are arrays; otherwise they are objects of data keyed by the field name.

#### Errors

An array of errors.

**Format:**

```
// Error structure
{
	type: "",     // A generalization of the error
	code: "",     // Standardized error code
	message: "",  // Human-readable details
	row: 0,       // Row index of parsed data where error is
	
}
```

#### Meta

```
```

### Extras

#### Config Object

This object defines settings, behaviors, and callbacks used during the parsing process. Any property that has not been specified will resort to the default value.
```
{
	delimiter: "",	// auto-detect
	newline: "",	// auto-detect
	quoteChar: '"',
	header: false,
	dynamicTyping: false,
	preview: 0,
	encoding: "",
	worker: false,
	comments: false,
	step: undefined,
	complete: undefined,
	error: undefined,
	download: false,
	skipEmptyLines: false,
	chunk: undefined,
	fastMode: undefined,
	beforeFirstChunk: undefined,
	withCredentials: undefined
}
```

**TODO smalers 2017-06-12 need Kory to fill out**

Provide overview, examples to create and parse CSV, also summarize the issues described in the CSV syntax page,
such as how to deal with missing values, quoted content, etc.  Use section breaks to make readable.
Link to relevant information.

MetaReader might be something to investigate.

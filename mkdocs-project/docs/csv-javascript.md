# Learn CSV / CSV with JavaScript #

This page provides information about using CSV format with JavaScript.

The following sections are available in this documentation:

* [JavaScript Language](#javascript-language) - reading and writing directly using JavaScript language
* [Papa Parse](#papa-parse) - a useful library

--------------

## JavaScript Language ##

**TODO smalers 2017-06-12 need to describe example of how to create and parse CSV using core JavaScript.
No need to provide complete solution but point out basics that illustrate why a library is helpful.**

## Papa Parse ##

Papa Parse is a fast and powerful, in-browser CSV parser that gracefully handles large files and malformed input. 

See also the [Papa Parse web page](http://papaparse.com).

The following sections provide useful examples for common tasks:

* [Convert CSV to JSON](#convert-csv-to-json)
	* [Parse string](#parse-string)
	* [Parse local file](#parse-local-file)
	* [Parse remote file](#parse-remote-file)
	* [Using jQuery to select files](#using-jquery-to-select-files)
* [Convert JSON to CSV](#convert-json-to-csv)
* [Config](#config)
* [Results](#results)
* [Missing Values](#missing-values)
* [Empty Lines](#empty-lines)
* [Comments in Data](#comments-in-data)

### Convert CSV to JSON ###

[JSON](http://www.json.org/) is a useful hierarchical data representation that works well with JavaScript.
Delimeted data can be parsed out of strings or files and converted to JSON using Papa Parse.
Files to be parsed can be local or remote.
This type of conversion will take a CSV file and convert it into a JSON object that contains the following properties:

* data
* errors
* meta 

#### Parse String ####

```javascript
Papa.parse(csvString[, config])
```

* **csvString** is a string delimited text to be parsed.
* **config** is an optional config object

**Example:**

```javascript
var parsed_string = Papa.parse("column1, column2, column3\n123,456,789");
console.log(parsed_string);
```

#### Parse Local File ####

```javascript
Papa.parse(file, config);
```
* **file** is a File object obtained from the DOM (Document Object Model).
* **config** is an optional config object

```javascript
Papa.parse(file, {
	complete: function(result){
		console.log(result);
	}
});
```
In the above example, the results are provided in the **complete** callback function. 

#### Parse Remote File ####

```javascript
Papa.parse(url, {
	download: true,
	// other configure options
});
```

* **url** is the path or URL to the file being downloaded.
* The second argument is a **config object** where **download: true** is set.
* The code above does not actually return anything. The results are provided asynchronously to a callback function.

***TODO smalers 2017-07-16 need Kory to update example to include the callback function.***

#### Using jQuery to Select Files ####

***TODO smalers 2017-07-16 Need Kory to provide more context.  What are we trying to do here and how does Papa do it?
It would be helpful to see example with data.***

When using jQuery include the latest jQuery Javascript file.

```javascript
<script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js"></script>
```

```javascript
$.get(file, function(result){
	var parsed_file = Papa.parse(result);
	console.log(parsed_file);
});
```
* **url** or **file path** to the file being parsed.
* **result** is the data being passed to Papa Parse

**Example:**

```javascript
$.get("test-data.csv",function(result){
	var parsed_file = Papa.parse(result);
	console.log(parsed_file);
});
```

### Convert JSON to CSV ###

Papa's unparse utility writes out correct CSV strings given an array of arrays or an array of objects. The unparse function will write these arrays to proper JSON.

***TODO smalers 2017-07-16 do you mean CSV at the end of the above sentence?
Label each of the following to explain what they are, such s Array of Arrays and it would be helpful to show the output for each example showing the final result.***


```javascript
Papa.unparse(data[, config]);
```

* Returns delimited text as a string.
* **data** is one of the following: 
	* Array of arrays
	* Array of objects
	* Object defining **fields** and **data**
* **config** is an optional config object

```javascript
var csv = Papa.unparse([
	["1-1","1-2","1-3"],
	["2-1","2-2","2-3"]
]);
console.log(csv);
```

```javascript
var csv = Papa.unparse([
	{
		"Column 1": "foo",
		"Column 2": "bar"
	},
	{
		"Column 1": "abc",
		"Column 2": "def"
	}
]);
console.log(csv);
```

```javascript
var csv = Papa.unparse({
	fields: ["Column 1", "Column 2"],
	data: [
		["foo", "bar"],
		["abc", "def"]
	]
});
console.log(csv);
```

### Config ###

The Papa Parse **parse** function may be passed a configuration object. This type of object defines settings, behavior, and callbacks used during the parsing process. Any properties that are left unspecified will be set to their default values.

```javascript
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

Refer to the following documentation for further explanation
[Config Documentation](http://papaparse.com/docs#config).

### Results ###

A parsed result will always contain the following three objects:

* **data**
* **errors**
* **meta**

Data and errors are arrays, and meta is an object. 

```javascript
{
	data:   // array of parsed data
	errors: // array of errors
	meta:   // object with extra info
}
```

***TODO smalers 2017-07-16 Can you explain more, perhaps with examples?
After all, the point of this documentation is to help programmers get to data that they can use.
Provide links to Papa Parse documentation if it makes sense.***

### Missing Values ###

***TODO smalers 2017-06-17 can you be more clear.  Discuss case with example of blank cell (two commas next to each other),
a string "null", and are there any other cases?"  What about NaN for numbers?***

Papa Parse does handle null and or missing values. However, when dealing with null, Papa Parse will parse it as a string.
This can be problematic when looking for null as an object rather than a string. 

**Example:**
```javascript
if(data[0] == null)
{
	// do something
}
```
```javascript
if(data[0] == "null")
{
	// do something
}
```

When dealing with missing values, Papa Parse will just insert an empty string ** "" **.

### Empty Lines ###

When dealing with empty lines, Papa Parse has an option that can be set to **true** in the config object being passed to the parse function.
If there are empty lines in a data file set the **skipEmptyLines** option to true.

```javascript
{
	skipEmptyLines: true // defaults to false
}
```

### Comments in Data ###

Comments in input data can be indicated in the configuration object similar to the following.
In this case any lines that start with `#` wil be ignored.

```javascript
{
	comments: '#' // Comment line indicator
}
```

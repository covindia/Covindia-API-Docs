# Documentation Convention

The [API Reference](api-reference.md) has all the end points that Covindia.com provides. All end points begin with `covindia` and are followed by hyphens (`-`). There are two types of data that Covindia provides with one exception.

* `covindia-history-*` - Data from the past until now
* `covindia-present-*` - Data at this moment in time

The exception is `covindia-raw-data` which provides all the data from the database.

Each end point has tables which give the key and the description of what the end point returns.

The data type of the is written in parantheses `(` and `)`. The data type corresponds to that cell of the table and not the value to which the key points.

There are end points that have keys that point to objects (analogous to dictionary of dictionaries in Python3). For making it easy, the description for these end points is across multiple tables. When one key points to an object, the description of the key leads to the Description Table of the object.

Keys can like \`key\` or key. The difference:

* \`key\` is the exact characters you can expect to find in the JSON that the end-point returns
* key is a placeholder for a general key that holds data.

Below is an example of the tables for easy understanding:

<table class="tg" style="undefined;table-layout: fixed; width: 708px">
<colgroup>
<col style="width: 150px">
<col style="width: 558px">
</colgroup>
	<tr>
		<th class="tg-fzdr">Table Example.1</th>
		<th class="tg-wo29"></th>
	</tr>
	<tr>
		<td class="tg-c2b5">Key<br></td>
		<td class="tg-c2b5">Description<br></td>
	</tr>
	<tr>
		<td class="tg-wo29">district-name (str)<br></td>
		<td class="tg-wo29">Each district-name (as defined in Resources) is the key to an object of type as described by Table Example.2<br></td>
	</tr>
</table>
<br>

<table class="tg" style="undefined;table-layout: fixed; width: 708px">
<colgroup>
<col style="width: 150px">
<col style="width: 558px">
</colgroup>
	<tr>
		<th class="tg-fzdr">Table Example.2</th>
		<th class="tg-wo29"></th>
	</tr>
	<tr>
		<td class="tg-c2b5">Key<br></td>
		<td class="tg-c2b5">Description<br></td>
	</tr>
	<tr>
		<td class="tg-wo29">`state` (str)<br></td>
		<td class="tg-wo29">(str) The state (as defined in Resources) the district is in.<br></td>
	</tr>
	<tr>
		<td class="tg-7seq">`infectedCount` (str)<br></td>
		<td class="tg-7seq">(int) The number of infected cases in this district until now.<br></td>
	</tr>
</table>
<br>

This would map to a JSON that looks like this:
```
{
	"Mumbai" : {
		"state" : "Maharastra",
		"infectedCount" : 100
	},
	"Bangalore" : {
		"state" : "Karnataka",
		"infectedCount" : 42
	},
	"Chennai" : {
		"state" : "Tamil Nadu",
		"infectedCount" : 55
	},
	...
}
```

<style type="text/css">
	.tg	{border-collapse:collapse;border-spacing:0;border-color:#ccc;text-align:justify;}
	.tg td{font-family: sans-serif;font-size:14px;padding:10px 7px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:#ccc;color:#333;background-color:#fff;}
	.tg th{font-family: sans-serif;font-size:14px;font-weight:normal;padding:10px 7px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:#ccc;color:#333;background-color:#f0f0f0;}
	.tg .tg-c2b5{background-color:#f9f9f9;font-weight:bold;border-color:#c0c0c0;text-align:center;vertical-align:top}
	.tg .tg-buh4{background-color:#f9f9f9;text-align:left;vertical-align:top}
	.tg .tg-fzdr{border-color:#c0c0c0;text-align:center;vertical-align:top}
	.tg .tg-wo29{border-color:#c0c0c0;text-align:left;vertical-align:top}
	.tg .tg-7seq{background-color:#f9f9f9;border-color:#c0c0c0;text-align:left;vertical-align:top}
	.tg .tg-0lax{text-align:left;vertical-align:top}
	.tg .tg-0pky{border-color:inherit;text-align:left;vertical-align:top}
	.tg .tg-btxf{background-color:#f9f9f9;border-color:inherit;text-align:left;vertical-align:top}
</style>
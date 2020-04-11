# API Reference - version 1.0.0

There are four API Endpoints that Covindia is providing at the moment:

* `covindia-raw-data`
* `covindia-history-district-data` (district-date-data)
* `covindia-present-general-data` (general-data)
* `covindia-present-state-data` (state-data)

It should be noted that these are all GET requests to be made at:

`https://v1.api.covindia.com/api-endpoint`

## covindia-raw-data
This returns a JSON object that contains raw data (as defined below). You need this when the other end-points don't satisfy your need.

<table class="tg" style="undefined;table-layout: fixed; width: 708px">
<colgroup>
<col style="width: 150px">
<col style="width: 558px">
</colgroup>
	<tr>
		<th class="tg-fzdr">Table CRD.1</th>
		<th class="tg-wo29"></th>
	</tr>
	<tr>
		<td class="tg-c2b5">Key<br></td>
		<td class="tg-c2b5">Description<br></td>
	</tr>
	<tr>
		<td class="tg-wo29">number (str)<br></td>
		<td class="tg-wo29">A string of a number which is the key to an object of type as described by Table CRD.2<br></td>
	</tr>
</table>
<br>

<table class="tg" style="undefined;table-layout: fixed; width: 708px">
<colgroup>
<col style="width: 150px">
<col style="width: 558px">
</colgroup>
	<tr>
		<th class="tg-fzdr">Table CRD.2</th>
		<th class="tg-wo29"></th>
	</tr>
	<tr>
		<td class="tg-c2b5">Key<br></td>
		<td class="tg-c2b5">Description<br></td>
	</tr>
	<tr>
		<td class="tg-wo29">`date` (str)<br></td>
		<td class="tg-wo29">(str) Date of case (either infected or death) as "DD/MM/YYYY"<br></td>
	</tr>
	<tr>
		<td class="tg-7seq">`time` (str)<br></td>
		<td class="tg-7seq">(str) Time of the report as "HH:MM". If this isn't known, it is usually the time of release of the source / entry. This shouldn't be taken as the time of the infection.<br></td>
	</tr>
	<tr>
		<td class="tg-0pky">`district` (str)<br></td>
		<td class="tg-0pky">(str) The name of the district according to the <span style="font-weight:bold">district list</span><br></td>
	</tr>
	<tr>
		<td class="tg-btxf">`state` (str)<br></td>
		<td class="tg-btxf">(str) The name of the state according to the <span style="font-weight:bold">state list</span><br></td>
	</tr>
	<tr>
		<td class="tg-0pky">`infected` (str)<br></td>
		<td class="tg-0pky">(int) The number of infected cases in this entry.<br></td>
	</tr>
	<tr>
		<td class="tg-btxf">`death` (str)<br></td>
		<td class="tg-btxf">(int) The number of deaths in this entry.</td>
	</tr>
	<tr>
		<td class="tg-0pky">`source` (str)<br></td>
		<td class="tg-0pky">(str) The source link for this entry.<br></td>
	</tr>
</table>
<br>
It is important to note that there may be multiple cases in a district in one day. Hence, all the values must be added up per date.
<br>

A GET request to `covindia-raw-data` returns a JSON of this format:
```
{
	"0" (str) : {
		"date" (str) : "dd/mm/YYYY" (str),
		"time" (str) : "HH:MM" (str),
		"district" (str) : "district-name-0" (str),
		"state" (str) : "state-name-0" (str),
		"infected": infected (int),
		"death" (str) : infected (int),
		"source" (str) : "source-link-0" (str)
	},
	"1" (str) : {
		"date" (str) : "dd/mm/YYYY" (str),
		"time" (str) : "HH:MM" (str),
		"district" (str) : "district-name-1" (str),
		"state" (str) : "state-name-1" (str),
		"infected": infected (int),
		"death" (str) : infected (int),
		"source" (str) : "source-link-1" (str)
	},
	...
}
```

## covindia-history-district-data
This returns a JSON object that contains dates as keys and corresponding districts' data. You need this when you ask, "What districts were affected on these dates?".

<table class="tg" style="undefined;table-layout: fixed; width: 708px">
<colgroup>
<col style="width: 150px">
<col style="width: 558px">
</colgroup>
	<tr>
		<th class="tg-c3ow">Table CDDD.1</th>
		<th class="tg-0pky"></th>
	</tr>
	<tr>
		<td class="tg-c2b5">Key<br></td>
		<td class="tg-c2b5">Description<br></td>
	</tr>
	<tr>
		<td class="tg-0pky">date (str)<br></td>
		<td class="tg-0pky">A string of the form "DD/MM/YYYY" which is the key to an object of type as described in Table CDDD.2<br></td>
	</tr>
</table>
<br>

<table class="tg" style="undefined;table-layout: fixed; width: 708px">
<colgroup>
<col style="width: 150px">
<col style="width: 558px">
</colgroup>
	<tr>
		<th class="tg-c3ow">Table CDDD.2</th>
		<th class="tg-0pky"></th>
	</tr>
	<tr>
		<td class="tg-c2b5">Key<br></td>
		<td class="tg-c2b5">Description<br></td>
	</tr>
	<tr>
		<td class="tg-0pky">district-name (str)<br></td>
		<td class="tg-0pky"><span style="font-weight:normal">Each district-name is a key to an object of type as decsribed in Table CDDD.3</span><br></td>
	</tr>
</table>
<br>

<table class="tg" style="undefined;table-layout: fixed; width: 708px">
<colgroup>
<col style="width: 150px">
<col style="width: 558px">
</colgroup>
	<tr>
		<th class="tg-c3ow">Table CDDD.3</th>
		<th class="tg-0pky"></th>
	</tr>
	<tr>
		<td class="tg-c2b5">Key<br></td>
		<td class="tg-c2b5">Description<br></td>
	</tr>
	<tr>
		<td class="tg-0pky">`infected` (str)</td>
		<td class="tg-0pky">(int) The total number of infected cases in this district till date (cumulative)<br></td>
	</tr>
	<tr>
		<td class="tg-buh4">`death` (str)<br></td>
		<td class="tg-buh4">(int) The total number of deaths in this district till date (cumulative)<br></td>
	</tr>
</table>

<br>

A GET request to `covindia-district-date-data` returns a JSON of this format:
```
{
	"DD/MM/YYYY" (str) : {
		"district-name-1" (str) : {
			"infected" : infected-value (int)
			"death" : death-value (int)
		},
		"district-name-2" (str) : {
			"infected" : infected-value (int)
			"death" : death-value (int)
		},
		...
	},
	"DD/MM/YYYY" (str) : {
		"district-name-1" (str) : {
			"infected" : infected-value (int)
			"death" : death-value (int)
		},
		"district-name-2" (str) : {general-
			"infected" : infected-value (int)
			"death" : death-value (int)
		},
		...
	}
}
```

## covindia-present-general-data
This returns a JSON object that contains general data (as defined below).


<table class="tg" style="undefined;table-layout: fixed; width: 708px">
<colgroup>
<col style="width: 150px">
<col style="width: 558px">
</colgroup>
	<tr>
		<th class="tg-fzdr">Table CGD.1</th>
		<th class="tg-wo29"></th>
	</tr>
	<tr>
		<td class="tg-c2b5">Key<br></td>
		<td class="tg-c2b5">Description<br></td>
	</tr>
	<tr>
		<td class="tg-wo29">`deathTotal` (str)<br></td>
		<td class="tg-wo29">(int) The total number of deaths until now.<br></td>
	</tr>
	<tr>
		<td class="tg-7seq">`districtList` (str)<br></td>
		<td class="tg-7seq">(array) An array containing strings where each string the name of a infected district.<br></td>
	</tr>
	<tr>
		<td class="tg-0lax">`infectedTotal` (str)<br></td>
		<td class="tg-0lax">(int) The total number of infected cases until now.<br></td>
	</tr>
	<tr>
		<td class="tg-buh4">`infectedMax` (str)<br></td>
		<td class="tg-buh4">(int) The maximum number of infected cases in a district across all districts.<br></td>
	</tr>
	<tr>
		<td class="tg-0lax">`lastUpdatedTime` (str)<br></td>
		<td class="tg-0lax">(str) A string representing the last updated time of the format<br> " YYYY-mm-dd HH:MM:SS.ffffff " <sup>#</sup>.<br></td>
	</tr>
	<tr>
		<td class="tg-buh4">`statesList` (str)<br></td>
		<td class="tg-buh4">(array) An array containing strings where each string the name of an infected state</td>
	</tr>
	<tr>
		<td class="tg-0lax">`totalCured` (str)<br></td>
		<td class="tg-0lax">(int) The number of cured people until now.<br></td>
	</tr>
</table>
<br>
<sup>#</sup> It may be important to note that this string is the output of `str(datetime.datetime.now())` in Python 3.6.9. To understand the directives, visit:
[https://strftime.org/](https://strftime.org/)


A GET request to `covindia-general-data` returns a JSON of this format:
```
{
	"deathTotal" (str) : death-total (int),
	"districtList" (str) : ["district-name-0" (str), "district-name-1" (str), ...] (array),
	"infectedTotal" (str) : infected-total (int),
	"infectedMax" (str) : infected-max (int),
	"lastUpdatedTime" (str) : "YYYY-mm-dd HH:MM:SS.ffffff" (str),
	"statesList" (str) : ["state-name-0" (str), "state-name-1" (str), ...] (array),
	"totalCured" (str) : total-cured (int)
}
```

## covindia-present-state-data
This returns a JSON object that contains states as keys along with the number of infected cases in that state. You need this when you
ask "What are the number of cases in this state right now?"

<table class="tg" style="undefined;table-layout: fixed; width: 708px">
<colgroup>
<col style="width: 150px">
<col style="width: 558px">
</colgroup>
	<tr>
		<th class="tg-fzdr">Table CSD.1</th>
		<th class="tg-wo29"></th>
	</tr>
	<tr>
		<td class="tg-c2b5">Key<br></td>
		<td class="tg-c2b5">Description<br></td>
	</tr>
	<tr>
		<td class="tg-wo29">state-name (str)<br></td>
		<td class="tg-wo29">(int) The total number of infected cases in this state.<br></td>
	</tr>
</table>
<br>

A GET request to `covindia-state-data` returns a JSON of this format:
```
	"state-name-0" : infected-number-0 (int),
	"state-name-1" : infected-number-1 (int),
	"state-name-2" : infected-number-2 (int),
	...
```

<style type="text/css">
	.tg {border-collapse:collapse;border-spacing:0;border-color:#ccc;text-align:justify;}
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
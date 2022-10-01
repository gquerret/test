## Description

Load binary data into database.

## XML namespace

`<pct:binary_load />`

## Parameters

| **Attribute**| **Description**|**Default value**|
|:-------------|:---------------|:---------------:|
|rebuildIndexes|Yes if indexes should be rebuild (build indexes option)|Yes               |
|indexRebuildTimeout|Timeout before rebuilding indexes (-G option)|0                 |
|paramFile|Parameter file|None|

† Only one of those attributes is mandatory
‡ Mandatory attribute

PCTBinaryLoad inherits attributes from [[PCT]].

## Parameters as nested elements

### [[DBConnection|PCTConnection]] (or [[PCTConnection]])

One and only one connection should be used with this task.

### [fileset](https://ant.apache.org/manual/Types/fileset.html)

Adds a file set to the file list to load

## Examples

None
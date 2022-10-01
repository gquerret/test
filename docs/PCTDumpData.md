## Description

Dump database table rows to a directory

## XML namespace

`<pct:data_dump />`

## Parameters

| **Attribute**| **Description**|**Default value**|
|:-------------|:---------------|:---------------:|
|destDir ‡     |Destination directory to dump data to|No default value  |
|tables        |Comma separated list of tables to dump|Blank means ALL   |
|encoding      |Set encoding to be used to dump data|If undefined or empty, -cpstream will be used|

† Only one of those attributes is mandatory
‡ Mandatory attribute

PCTDumpData inherits attributes from [PCT](PCT.md) and [PCTRun](PCTRun.md). However, PCTDumpData must have one and only one [PCTConnection](PCTConnection.md).

## Parameters as nested elements

None

## Examples

```xml
<PCTDumpData destDir="datas" dlcHome="${env.DLC}">
  <PCTConnection dbName="test" singleUser="true" />
</PCTDumpData>
```
Connects in single-user mode to test.db and dumps each table's data into datas directory

```xml
<PCTDumpData destDir="datas" tables="Tab1,Tab2" dlcHome="${env.DLC}">
  <PCTConnection dbName="test" singleUser="true" />
</PCTDumpData>
```
Same as previous, but dumps only Tab1 and Tab2
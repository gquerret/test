## Description

Create binary dump (.bd) files using `proutil -C dump`. Tables starting with `_` and `SYS` are always ignored.

## XML namespace

`<pct:binary_dump />`

## Parameters

| **Attribute**| **Description**|**Default value**|
|:-------------|:---------------|:--------:|
|dest   ‡      |Destination directory|None|

† Only one of those attributes is mandatory
‡ Mandatory attribute

PCTBinaryDump inherits attributes from [[PCT]].

## Parameters as nested elements

### [[PCTConnection]]

One and only one connection should be used with this task.

### include and exclude

Comma-separated list of patterns of tables that must be included/excluded ; all tables are included when include is omitted

## Examples

```xml
<PCTBinaryDump dest="outputDir">
  <PCTConnection dbName="foo" dbDir="base" singleUser="true" />
</PCTBinaryDump>
```
Dump every table in foo database.

```xml
<PCTBinaryDump dest="outputDir">
  <PCTConnection dbName="foo" dbDir="base" singleUser="true" />
  <exclude name="b*" />
  <include name="ba*" />
</PCTBinaryDump>
```
Dump every table in foo database, excluding those starting with the letter b. Tables starting with "ba" will be included.
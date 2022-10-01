## Description
Creates a sports2000 database

## XML namespace
`<pct:sports2000 />`

## Parameters

| **Attribute**| **Description**| **Default value**|
|:-------------|:---------------|:---------------|
|dbName ‡        |Database name   | |
|destDir       |Destination directory where to create the database| Current work directory.|

† Only one of those attributes is mandatory ‡ Mandatory attribute

PCTCreateBase inherits attributes from [[PCT]].

## Parameters as nested elements

## Examples
```xml
<sports2000 dbName="sp2k" destDir="db" dlcHome="${DLC}" />
```
Creates a copy of sports2000 database named sp2k in `db` directory.
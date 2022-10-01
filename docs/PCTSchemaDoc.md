## Description

Creates XML documentation from database. This XML file is meant to be transformed using a XSL stylesheet, like [this one](https://raw.githubusercontent.com/Riverside-Software/pct/master/SchemaDoc.xsl). See examples below for a complete process. You can find an sample for sports2000 database [here](http://riverside-software.fr/doc/sports2000/index.html).

## XML namespace

`<pct:schema_doc />`

## Parameters

| **Attribute**| **Description**|**Default value**|
|:-------------|:---------------|:---------------:|
| file ‡ | XML file to be generated |No default value  |

† Only one of those attributes is mandatory
‡ Mandatory attribute

PCTSchemaDoc inherits attributes from [PCT](PCT.md) and [PCTRun](PCTRun.md). However, PCTSchemaDoc must have one and only one [PCTConnection](PCTConnection.md).

## Parameters as nested elements

None

## Examples

```xml
<PCTSchemaDoc file="doc/db.xml">
  <PCTConnection dbName="MyDB" dbDir="base"/>
</PCTSchemaDoc>
<xslt in="doc/db.xml" style="doc/SchemaDoc.xsl" out="doc/output.txt">
  <param name="outputdir" expression="doc/MyDB"/>
  <param name="dbname" expression="MyDB" />
</xslt>
```
Creates an XML file `doc/db.xml` which is transformed using `doc/SchemaDoc.xsl` to produce HTML documentation in `doc/MyDB` directory.
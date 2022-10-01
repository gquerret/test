## Description

Generates JSON documentation from OpenEdge classes. Comments have to be written using a specific syntax to be parsed correctly; documentation is [here](StandardCommentBlock). This task also requires access to rcode.

## XML namespace

`<pct:json_doc />`

### Parameters

| **Attribute**| **Description**| **Default value**|
|:-------------|:---------------|:---------------:|
|destFile ‡    |JSON file output|No default value  |
|buildDir ‡    |Directory where rcode will be read|No default value|
|encoding      |Use specified encoding when reading source files. Not yet implemented|No default value|
|indent        |JSON pretty-printing|False|

† Only one of those attributes is mandatory
‡ Mandatory attribute

ClassDocumentation inherits attributes from [[PCT]].

## Parameters as nested elements

### fileset

Standard Ant fileset

### propath

Standard Ant path structure

### DBConnection and DBConnectionSet


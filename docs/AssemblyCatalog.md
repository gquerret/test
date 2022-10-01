## Description

Generate JSON file with the description of all classes, properties and methods in the referenced assemblies.xml file. JSON output is used by [CABL](https://github.com/Riverside-Software/sonar-openedge) to help the analysis of source.

## Parameters

| **Attribute**| **Description**|**Default value**|
|:-------------|:---------------|:---------------:|
| destFile | Output file | No default value |

AssemblyCatalog inherits attributes from [[PCT]] and [[PCTRun]].

## Parameters as nested elements

None

## Example

```xml
<AssemblyCatalog dlcHome="${DLC}" assemblies="path/to/dir/with/assemblies.xml" destFile="catalog.json" />
```

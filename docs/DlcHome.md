## Description

Define the OpenEdge installation directory. When the value is set, you don't have to define dlcHome attribute anymore in the rest of the build.
This task also adds `/.pct/` to the default excluded files.

## XML namespace

`<pct:dlc_home />`

## Parameters

| **Attribute**| **Description**|**Default value**|
|:-------------|:---------------|:--------:|
| value ‡ |OpenEdge installation directory|None|

‡ Mandatory attribute

## Parameters as nested elements
None

## Examples

### Example 1
```xml
<DlcHome value="/path/to/dlc" />
```
Will use `/path/to/dlc` in any subsequent PCT task.
### Example 2
```xml
<DlcHome value="${DLC}" />
```
Will use the content of the DLC variable in any subsequent PCT task. This DLC variable is usually passed from the command line:
```
ant -DDLC=/path/to/dlc targetName
```
### Example 3
```xml
<property environment="env"/>
<DlcHome value=${env.DLC}" />
```
Will use the content of the DLC environment variable in any subsequent PCT task.
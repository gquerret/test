## Description

Exports OpenEdge Mobile or REST applications.

⚠️ This task can't be used with OpenEdge 12.0 and above ; the following code should be used (tested with 12.2.2):
```xml
<!-- Additional tasks declaration ; version numbers may depend on OE version -->
<taskdef resource="com/progress/openedge/pdt/ant/ablwebapp/ablwebapps.properties">
  <classpath>
    <pathelement location="${DLC}/java/ant-ablwebapp.jar" />
    <pathelement location="${DLC}/java/1padapters-idl.jar" />
    <pathelement location="${DLC}/java/1padapters-util.jar" />
    <pathelement location="${DLC}/java/ant-libs/ablwebapp.jar" />
    <pathelement location="${DLC}/java/ant-libs/ablwebapp-dependencies.jar" />
    <pathelement location="${DLC}/java/ant-libs/codemodel-dependencies.jar" />
    <pathelement location="${DLC}/java/ant-libs/ast.jar" />
    <pathelement location="${DLC}/java/ant-libs/ast-dependencies.jar" />
    <pathelement location="${DLC}/java/ant-libs/velocity-1.7.jar" />
    <pathelement location="${DLC}/java/ant-libs/velocity-1.7-dep.jar" />
    <pathelement location="${DLC}/java/ant-libs/1padapters-restExpose.jar" />
    <pathelement location="${DLC}/java/ext/jettison-1.4.0.jar" />
    <pathelement location="${DLC}/java/ext/commons-logging-1.2.jar" />
    <pathelement location="${DLC}/java/ext/xmlschema-core-2.2.1.jar" />
  </classpath>
</taskdef>
<!-- RestGen.projectDir goes to PaarGeneration.srcdir -->
<!-- RestGen.destFile goes to PaarGeneration.destdir -->
<!-- RestGen.services goes to PaarGeneration.services -->
<PaarGeneration srcdir="." dlc="${DLC}" verbose="true" destdir="dist" services="RestProjectService" />
```

The other option is to move your code to Web Handlers. 

## XML namespace

`<pct:restgen />`

## Parameters

| **Attribute**| **Description**|**Default value**|
|:-------------|:---------------|:---------------:|
| projectDir ‡ |Project directory name (with .services directory)|None|
| services ‡ |Colon separated list of Service names|None|
| type ‡ |One of ```paar```, ```mobpaar```, ```restwar```, ```mobwar```, ```mobappwar```, ```onlymobapp```| |
| destFile ‡ | Destination file name | |
| includeJars | Include JARs from `$DLC/rest/lib` | False |

† Only one of those attributes is mandatory ‡ Mandatory attribute

## Parameters as nested elements
None

## Examples

### Example 1
```xml
<RestGen dlcHome="${DLC}" projectDir="." destFile="dist/REST.zip" type="paar" services="RestProjectService" />
```
Will generate PAAR file for RestProjectService in current directory
### Example 2
```xml
<RestGen dlcHome="${DLC}" projectDir="." destFile="dist/REST.zip" type="paar" services="RestProjectService" pdsHome="/path/to/oeide" />
```
Same as previous example, but will use Eclipse JAR files from /path/to/oeide. This directory needs to be a copy of the directory of the same name on a Windows installation. Useful for UNIX REST generation.
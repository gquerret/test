### Description

A special [Fileset](http://ant.apache.org/manual/Types/fileset.html) meant to extract files from a procedure library.

### Parameters

| **Attribute**| **Description**| **Default value**|
|:-------------|:---------------|:--------:|
|src ‡         |Specify a PL file whose contents will be extracted| None |

† Only one of those attributes is mandatory ‡ Mandatory attribute

### Parameters as nested elements

None

### Examples

```xml
<!-- Don't forget to declare types -->
<typedef resource="types.properties" />

<target name="copy">
  <copy todir="destDir">
    <plfileset src="${DLC}/gui/adeuib.pl" includes="**/*.r" />
    <!-- You can mix plfilesets with any other fileset type -->
    <fileset dir="build" includes="**/*.r" />
  </copy>
</target>
```
Will extract any .r files from `$DLC/gui/adeuib.pl` to destDir
## Description

Run an ABLUnit tests sequence. For further information, refer to the progress documentation.

## XML namespace

`<pct:ablunit />`

## Parameters

| **Attribute**| **Description**|**Default value**|
|:-------------|:---------------|:---------------:|
|destDir | Directory where to put result file. Don't use destDir under Linux, as a bug prevents results.xml from being generated | Base directory |
|writeLog | Creates `ablunit.log` in temp directory in case of error | False |
|haltOnFailure | Stop the build process if a test fails (errors are considered failures as well) | False |

† Only one of those attributes is mandatory
‡ Mandatory attribute

ABLUnit inherits attributes from [[PCT]] and [[PCTRun]].

## Parameters as nested elements

### [Fileset](http://ant.apache.org/manual/Types/fileset.html)

Support the standard Ant Fileset to get a set of test files.

### Examples 1

```xml
<ABLUnit>
  <fileset dir="src" includes="**/*.p" />
  <fileset dir="src2" includes="**/*.cls" />
  <propath>
    <pathelement path="src" />
    <pathelement path="src2" />
    <!-- When running on OE up to 11.3, don't forget to include ablunit.pl and OpenEdge.Core.pl in your propath
    <pathelement location="/path/to/ablunit.pl" />
    <pathelement location="/path/to/OpenEdge.Core.pl" /> -->
  </propath>
</ABLUnit>
```
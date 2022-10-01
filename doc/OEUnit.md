## Description

Run an OEUnit tests sequence. For further informations, refer to [OEUnit website](https://github.com/CameronWills/OEUnit).

Will run every tests from classes sent by a fileset and put results in a report file (xml,csv,txt).

## XML namespace

`<pct:OEUnit />`

## Parameters

| **Attribute**| **Description**|**Default value**|
|:-------------|:---------------|:---------------:|
|destDir ‡     |Directory where to put result file|Base directory    |
|format        |Format of report file : JUnit, SureFire, CSV, Text|JUnit             |

† Only one of those attributes is mandatory ‡ Mandatory attribute

## Parameters as nested elements

### [Fileset](http://ant.apache.org/manual/Types/fileset.html)

Support the standard Ant Fileset to get a set of test classes. Can be test file or test suite.

## Examples

```xml
<OEUnit destDir="test-reports" format="junit">
  <fileset dir="src" includes="**/*.cls" />
  <propath>
    <pathelement path="src" />
    <pathelement path="/path/to/OEUnit" />
  </propath>
</OEUnit>
```
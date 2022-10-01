## Description

Defines profiler options

## Parameters

| **Attribute**| **Description**| **Default value**|
|:-------------|:---------------|:-----------------|
|enabled ‡ |Enables or disables profiler|False             |
|description   |Description of profiler session|Default description|
|outputDir †   |Generates a profiler output in this directory, with a unique name|No default value  |
|outputFile †  |Profiler output file name|No default value  |
|coverage      |Enables code coverage|False             |
|statistics    |Enables statistics|False             |
|listings      |Generates debug listing files in this directory|No default value  |

† Only one of those attributes is mandatory ‡ Mandatory attribute

## Parameters as nested elements

None

## Examples
```xml
<PCTRun procedure="tests.p">
  <Profiler enabled="true" outputDir="profiler" coverage="true" />
</PCTRun>
```
Executes this session with profiler, generating a unique file name in profiler directory (called for example profiler123456.out), with code coverage activated.
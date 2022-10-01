## Description

Dumps sequences from a database to a directory.

There is no dedicated task to load sequences, but you can use PCTRun for that An example is available [here](https://github.com/Riverside-Software/pct/issues/402).

## XML namespace

`<pct:sequences_dump />`

## Parameters

| **Attribute**| **Description**|
|:-------------|:---------------|
|destDir ‡       |Destination directory where to dump sequences (file name is always `_seqvals.d`)|
|encoding      |Set encoding to be used to dump data. If attribute is not set or empty, then -cpstream will be used|

† Only one of those attributes is mandatory ‡ Mandatory attribute

PCTDumpSequences inherits attributes from [[PCT]] and [[PCTRun]]. However, PCTDumpSequences must have one and only one [[PCTConnection]].

## Parameters as nested elements

None

## Examples

```xml
<PCTDumpSequences destDir="datas" dlcHome="${env.DLC}">
  <PCTConnection dbName="test" singleUser="true" />
</PCTDumpSequences>
```
Connects in single-user mode to test.db and dumps sequences current value into datas directory

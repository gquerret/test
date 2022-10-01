## Description

Dump database schema to file.

## XML namespace

`<pct:schema_dump />`

## Parameters

| **Attribute**| **Description**|
|:-------------|:---------------|
|destFile ‡     |Destination file to dump the schema|
|tables        |Dumps only the selected tables. Comma-separated list||

† Only one of those attributes is mandatory ‡ Mandatory attribute

PCTDumpSchema inherits attributes from [[PCT]] and [[PCTRun]]. However, PCTDumpSchema must have one and only one [[PCTConnection]].

## Parameters as nested elements

### Table

Dumps a specific table. Merged with the `tables` attribute.

## Examples
```xml
<PCTDumpSchema destFile="schema.df" dlcHome="${DLC}">
  <PCTConnection dbName="test" singleUser="true" />
</PCTDumpSchema>
```
Connects in single-user mode to test.db and dumps schema to schema.df

Can be followed by:
```xml
<copy file="schema.df" tofile="schema.df">
  <filterchain>
    <tailfilter lines="-1" skip="6" />
  </filterchain>
</copy>
```
To remove the useless and cumbersome trailer from the dump file. 
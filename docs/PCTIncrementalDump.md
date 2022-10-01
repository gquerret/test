## Description

Creates a schema diff file between two databases. This is a wrapper around `prodict/dump_inc.p`.

## XML namespace

`<pct:incr_dump />`

## Parameters

| **Attribute**| **Description**| **Default value**|
|:-------------|:---------------|:--------:|
|destFile ‡     |File containing the schema dump|None|
|renameFile    |The renameFile parameter is used to identify tables, database fields and sequences that have changed names, [See progress knowledge base article P103489 for the format. ](https://knowledgebase.progress.com/articles/Knowledge/P103489)|None  |
|debugLevel    |Debug level (0, 1 or 2 (verbose))|0                 |
|activeIndexes |0 if all indexes should be created active (0), 1 if only unique indexes should be created inactive, or 2 to create all indexes inactive|0                 |
|removeEmptyDFFile|True to remove the generated DF file if there are no schema differences |False             |

† Only one of those attributes is mandatory ‡ Mandatory attribute

PCTIncrementalDump inherits attributes from [[PCT]] and [[PCTRun]].

## Parameters as nested elements

PCTIncrementalDump previously accepted PCTConnection nodes with specific aliases, but they are  now deprecated. Use sourceDb and targetDb nodes instead.

### [SourceDb](PCTConnection)

Database to migrate from

### [TargetDb](PCTConnection)

Database to migrate to

## Examples

```xml
<PCTIncrementalDump destFile="incr.df">
  <SourceDb dbName="db1" singleUser="true" />
  <TargetDb dbName="db2" singleUser="true" />
</PCTIncrementalDump>
```
Compares db1 to db2, and generates a diff named incr.df, which could be loaded into db2 to bring it to same schema as db1.
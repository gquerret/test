## Description

Loads database schema.

## XML namespace

`<pct:schema_load />`

## Parameters

| **Attribute**| **Description**|**Default value**|
|:-------------|:---------------|:---------------:|
| srcFile ‡    |DF file to be loaded|None|
|unfreeze      |Unfreeze the tables in the database before loading the schema, then refreeze everything that was unfrozen after the load.|False|
|onlineChanges |Relaxes requirements to apply online changes (use `SESSION:SCHEMA-CHANGE = 'NEW OBJECTS'`). |False|
|commitWhenErrors|Commits transaction even if there are errors. If set to true and there are errors, it just displays a warning. If set to false and there are errors, build fails.|False|
|callbackClass      |Implementation of `rssw.pct.ILoadCallback`. Only for OpenEdge 11.3+|None|
|analyzerClass      |Implementation of `OpenEdge.DataAdmin.Binding.IDataDefinitionLoader`. Only for OpenEdge 11.3+|None|

† Only one of those attributes is mandatory ‡ Mandatory attribute

PCTLoadSchema inherits attributes from [[PCT]] and [[PCTRun]].

## Parameters as nested elements

### [Resource Collection](http://ant.apache.org/manual/Types/resources.html#collection)

Adds a resource collection to be loaded in database

## Callback class

Callback class has to implement [`rssw.pct.ILoadCallback`](https://github.com/Riverside-Software/pct/blob/master/src/progress/rssw/pct/ILoadCallback.cls) or extend [`rssw.pct.AbstractLoadCallback`](https://github.com/Riverside-Software/pct/blob/master/src/progress/rssw/pct/AbstractLoadCallback.cls), and have a no-arguments constructor.

## Analyzer class

Class has to implement [`OpenEdge.DataAdmin.Binding.IDataDefinitionLoader`](https://documentation.progress.com/output/oehttpclient/oe117/index.html?OpenEdge.DataAdmin.Binding.IDataDefinitionLoader.html).

## Examples

```xml
<PCTLoadSchema srcFile="schema.df" dlcHome="${DLC}">
  <PCTConnection dbName="test" singleUser="true" />
</PCTLoadSchema>
```
Connects in single-user mode to test.db and loads schema from schema.df

```xml
<PCTLoadSchema dlcHome="${DLC}">
  <PCTConnection dbName="test" singleUser="true" />
  <fileset dir="schema" includes="*.df" />
</PCTLoadSchema>
```
Connects in single-user mode to test.db and loads every .df file in schema directory
## Description

Load tables data from plain .d files

## XML namespace

`<pct:data_load />`

## Parameters

| **Attribute**| **Description**| **Default value**|
|:-------------|:---------------|:---------------:|
|srcDir †      |Source directory to load data from|No default value  |
|srcFile †     |Source file to load data from|No default value  |
|tables        |Comma separated list of tables to load. Only used with srcDir attribute|Blank means ALL   |
|table         |Table name. Only used with srcFile attribute|No default value  |
|callbackClass |Callback class for the data load procedure. Only under OE 11.3+|No default value  |
|errorTolerance|Acceptable error percentage (must be between 0 and 100)|0                 |
|silent        |Quiet log output|False|

† Only one of those attributes is mandatory
‡ Mandatory attribute

PCTLoadData inherits attributes from [[PCT]] and [[PCTRun]].

## Parameters as nested elements

### Table

Loads a specific table. If no Table nodes are used, then PCTLoadData tries to load every table in dictionary.

## Callback class

Callback class has to implement `rssw.pct.ILoadDataCallback` or extend `rssw.pct.AbstractLoadDataCallback`, and have a no-arguments constructor.
The interface is :
```
  method public void beforeLoad(f as char).
  method public void afterLoad(f as char, logger as rssw.pct.LoadDataLogger).
```

An example class doing a full backup of the table before loading data and restoring data in case of failure is available [here](https://github.com/Riverside-Software/pct/blob/master/src/progress/rssw/pct/BackupDataCallback.cls)

## Examples

### Example 1
```xml
<PCTLoadData srcDir="data" dlcHome="${DLC}">
  <DBConnection dbName="test" singleUser="true" />
</PCTLoadData>
```
Connects in single-user mode to test.db and loads each file from data directory in it

### Example 2
```xml
<PCTLoadData srcDir="data" dlcHome="${DLC}">
  <DBConnection dbName="test" singleUser="true" />
  <Table name="Table1" />
  <Table name="Table2" />
</PCTLoadData>
```
Connects in single-user mode to test.db and tries to load only Table1.d and Table2.d from data directory. If Table3 is present in dictionary, and Table3.d is present in data directory, then this file will be skipped.

### Example 3

```xml
<PCTLoadDataCallback srcFile="data/NewDataForTab1.d" table="Tab1" callbackProcedure="MyLogger" dlcHome="${DLC}">
  <DBConnection dbName="test" singleUser="true" />
</PCTLoadDataCallback>
```
Connect in single-user mode to test.db, then load records from data/NewDataForTab1.d and using MyLogger class as a callback

Class MyLogger (which has to be found in propath) could be :
```
 method public override void afterLoad(f as char, logger as rssw.pct.LoadDataLogger):
  if logger:loadException or logger:bailed then copy-lob from logger:getErrors() to file "dataload.txt".
 end method.
```
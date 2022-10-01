## Description

Add a database connection. Both PCTConnection and DBConnection can be used.

## XML namespace

`<pct:dbConnection />` or `<pct:db_connection />`

## Parameters

| **Attribute**| **Description**| **Default value**|
|:-------------|:---------------|:----------------:|
|dbName †       |Database physical name|None|
|paramFile †    |Parameter file (-pf parameter). If paramFile is set and dbName is unset, paramFile is always in first position. If both paramFile and dbName are set, dbName is in first position and paramFile in second position. Don't define multiple database connections in a single paramFile, this can lead to unexpected behavior.|None|
|dbDir         |Directory where database is physically located (relative to baseDir)|None |
|dbPort        |TCP port to connect to (-S parameter)|None|
|protocol      |Protocol to use (-N parameter)|None|
|logicalName   |Logical name for the database (-ld parameter)|None|
|cacheFile     |Name of the binary cache file (-cache parameter)|None|
|dataService   |Dataservice (-DataService parameter)|None|
|dbType        |Database type (Oracle, SQL Server, ...) (-dt parameter)|None|
|hostName      |Host name where the database resides (-H parameter)|None|
|userName      |Login (-U parameter)|None|
|password      |Password (-P parameter)|None|
|readOnly      |Open the database in read-only mode (-RO parameter)|False|
|singleUser    |Open the database in single-user mode (-1 parameter)|False|

† Only one of those attributes is mandatory
‡ Mandatory attribute

## Parameters as nested elements

### [[Alias|PCTAlias]] (or [[PCTAlias]])

Add an alias to a connection

## References

As of build #165, it is possible to define database connection references. When using references, you may override some parameters (singleUser and readOnly). Other parameters are appended. Attributes dbName and dbDir can never be overridden.

## Examples
```xml
<PCTRun ...>
  <PCTConnection dbName="foo" logicalName="bar" paramFile="conf/param.pf"/>
  <!-- DBConnection type is identical to PCTConnection -->
  <DBConnection dbName="db2" dbDir="." />
</PCTRun>
```
On the command line will be appended the following parameters : `-db foo -pf conf/param.pf -ld bar -db db2`

```xml
<project>
  <!-- Define a first connection -->
  <DBConnection id="db1" dbName="foo" hostname="localhost" dbPort="10000" />
  <!-- Define a second connection with one alias -->
  <DBConnection id="db2" dbName="bar" dbDir="/var/db" singleUser="true">
    <Alias name="db3" />
  </DBConnection>

  <target name="build">
    <!-- Execute with only one database connected -->
    <PCTRun procedure="...">
      <DBConnection refid="db1" />
    </PCTRun>
    <PCTCompile destDir="build">
      <!-- Use first referenced connection, and add one alias -->
      <DBConnection refid="db1">
        <Alias name="db4" />
      </DBConnection>
      <!-- Second connection, alias db3 remains defined and -1 parameter is removed -->
      <DBConnection refid="db2" singleUser="false" />
    </PCTCompile>
  </target>
</project>
```
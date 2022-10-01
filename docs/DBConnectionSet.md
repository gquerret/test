# DBConnectionSet type

## XML namespace

`<pct:dbConnectionSet />` or `<pct:db_connection_set />`

## Description

Creates a set of database connections, which can be referenced later by PCT tasks.

## Parameters

| **Attribute**| **Description**| **Type**| **Requirement**| **Default value**|
|:-------------|:---------------|:--------|:---------------|:-----------------|
|id            |ID of this set  |String   |Required        |No default value  |

## Parameters as nested elements

### [DBConnection](PCTConnection) (or [PCTConnection](PCTConnection))

Adds a database connection to this set

## Examples
```xml
<!-- Don't forget to declare types -->
<typedef resource="types.properties" />

<DBConnectionSet id="myset">
  <DBConnection dbName="db1" dbDir="db" />
  <DBConnection dbName="db2" dbDir="db">
    <Alias name="foo" />
  </DBConnection>
</DBConnectionSet>
<PCTRun ...>
  <DBConnectionSet refid="myset" />
</PCTRun>
```
## Description

Creates Progress database.

## XML namespace

`<pct:db_create />`

## Parameters

| **Attribute**| **Description**|Default value|
|:-------------|:---------------|:---------------:|
| dbName ‡      |Database name |None|
|destDir       |Destination directory where to create the database.|Project basedir|
|sourceDb      |Copy specified DB to target DB.|If attribute is not provided, the empty DB will be used|
|schemaFile    |Initial dump file(s) to load into database. Separate dump filenames with commas. Files are resolved first as an absolute path, then relative to base directory. Wildcards are not expanded|None|
|structFile    |Structure description file.|None|
|blockSize     |Block size in kilobytes (1, 2, 4 or 8). Can't be used with sourceDb attribute|8|
|noInit        |No initialization of database schema (`procopy emptyX dbName`). Can't be used with sourceDb attribute.|False|
|codepage      |Copy empty database from a prolang subdirectory. Can't be used with sourceDb attribute.|None|
|wordRules     |Assign a specific word rules table to a database (ie runs a `proutil dbname -C word-rules XXX`). This command is run before loading schema (if available). |None|
|multiTenant   |Enable multitenancy for this database. |False|
|failOnError   |Only during schema load. |True|
|collation     |Load collation table (copy from `$DLC/prolang` or `$DLC/prolang/codepage`)|None|
|tempDir       |-T parameter when loading schema|None|
|cpInternal    |-cpinternal parameter when loading schema|None|
|cpStream      |-cpstream parameter when loading schema|None|
|cpCase        |-cpcase parameter when loading schema|None|
|cpColl        |-cpcoll parameter when loading schema|None|
|newInstance   |Appends `-newInstance` in the procopy command line. |False|
|largeFiles    |Enable large files for this database. |False|
|relative      |Appends `-relative` in the procopy command line. |False|
|auditing      |Enable auditing for this database. |False|
|auditArea     |Audit tables area name|None|
|auditIndexArea|Audit indexes area name|None|

† Only one of those attributes is mandatory ‡ Mandatory attribute

PCTCreateDatabase inherits attributes from [[PCT]].

## Parameters as nested elements

### [Resource Collection](http://ant.apache.org/manual/Types/resources.html#collection)

Load additional DF files after having created the database.

### [propath](http://ant.apache.org/manual/using.html#path)

Creates a nested propath, and adds it to the implicit propath. The propath is only used during schema update.

### [[OracleHolder|Holder]]

Creates a new Oracle schema holder inside a database. If a schema holder is defined, no schema can be loaded in the main database.

### [[MSSHolder|Holder]]

Creates a new SQL Server schema holder inside a database. If a schema holder is defined, no schema can be loaded in the main database.

### [[ODBCHolder|Holder]]

Creates a new ODBC schema holder inside a database. If a schema holder is defined, no schema can be loaded in the main database.

## Examples
```xml
<PCTCreateDatabase dbName="MyDB" dlcHome="${env.DLC}" />
```
Creates an empty database named MyDB in current directory. Command line used is `procopy empty8 MyDB`

```xml
<PCTCreateDatabase dbName="MyDB" destDir="MyDir" dlcHome="${env.DLC}" schemaFile="/home/test/MySchema.df" wordRules="1">
  <sort>
    <fileset dir="foo" includes="*.df" />
    <reverse xmlns="antlib:org.apache.tools.ant.types.resources.comparators">
      <date />
    </reverse>
  </sort>
</PCTCreateDatabase >
```
Creates an empty database named MyDB in MyDir subdir of the current directory, then load proword.1 word break table (`_proutil MyDB -C word-rules 1`), and then loads schema from /home/test/MySchema.df, followed by every .df file in directory `foo`, sorted by descending modification date.

```xml
<echo file="test.st">
  b test.b1 f 1024
  b test.b2 v 2048
  d "Schema Area":6,64 test.d1 f 1024
  d "Schema Area":6,64 test.d2 v 2048
</echo>
<PCTCreateDatabase dbName="test" dlcHome="${env.DLC}" structFile="test.st" codepage="utf" />
```
Creates a database structure from test.st file (`_proutil prostrct create test test.st`) and then `procopy $DLC/prolang/utf/empty8 test`.

```xml
<PCTCreateDatabase dbName="test" dlcHome="${DLC}" sourceDb="/riverside/db/mydb" schemaFile="add.df" />
```
Copy `/riverside/db/mydb` to `test.db` in current directory, then load `add.df` in this new database
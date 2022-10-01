## Description

Executes a Progress procedure.

This task generates a temporary Progress procedure on the fly which sets the propath and declares database aliases according to specified parameters, and then runs the specified procedure.

This temporary procedure is launched by an Exec task (using either `prowin`, `prowin32` or `_progres` executable), and with the specified arguments.

You need to add `RETURN "IntegerValue"` at the end of your procedure. This return value is read by PCT, and any non-zero value tells Ant to throw an exception (thus stopping the build).
* Database connection problems ⇒ return value 14
* Errors during execution of your procedure ⇒ return value 1
* QUIT statement ⇒ return value 66

## XML namespace

`<pct:run />`

## Parameters

| **Attribute**| **Description**|**Default value**|
|:-------------|:---------------|:---------------:|
| procedure ‡ |Procedure to execute|None|
|graphicalMode |True if you want to execute procedure using `prowin32` (or `prowin` on 64 bits platforms), `_progres` otherwise.|False|
|baseDir       |The directory in which the OpenEdge runtime should be executed. File attributes (such as paramFile or iniFile) are still resolved against the project base directory. |_Project's basedir_|
|failOnError   |True to throw a build exception if the OpenEdge procedure exits with a return value other than 0.|True|
|resultProperty|The name of a property in which the return code of the Progress procedure should be stored. Only of interest if failOnError is set to false.|None|
|noErrorOnQuit |Set to true to prevent PCT from returning an error (code 66) when a QUIT statement is executed|False|
|mainCallback  |Callback class (implementation of `rssw.pct.IMainCallback`)|None|
|xCodeSessionKey | `SECURITY-POLICY:XCODE-SESSION-KEY` attribute|None|
|debugPCT      |True to keep internal temporary files on disk.|False|

† Only one of those attributes is mandatory
‡ Mandatory attribute

## OpenEdge parameters

Those parameters are mapped to OpenEdge parameters, so they don't **directly** relate to PCT.

| **Attribute**| **Description**|**Default value**|
|:-------------|:---------------|:---------------:|
|iniFile       |INI file (adds -basekey INI -ininame ...). Attribute is skipped if file can't be found|None|
|cpInternal    |Internal code page (-cpinternal parameter)|None|
|cpStream      |Stream code page (-cpstream parameter)|None|
|cpColl        |Collation table (-cpcoll parameter)|None|
|cpCase        |Case table (-cpcase parameter)|None|
|NumSep        |Thousands separator. Can be either a numeric value or a character, e.g. numsep="44" or numsep=","|None|
|NumDec        |Fractional separator. Can be either a numeric value or a character, e.g. numdec="46" or numdec="."|None|
|centuryYearOffset|Century Year Offset (-yy parameter)|None|
|parameter     |Parameter (-param parameter)|None|
|dirSize       |The number of compiled procedure directory entries (-D parameter)|None|
|inputChars    |The number of characters allowed in a single statement (-inp parameter)|None|
|maximumMemory |The amount of memory allocated for r-code segments (-mmax parameter)|None|
|stackSize     |Stack size in 1KB units (-s parameter)|None|
|token         |The number of tokens allowed in a 4GL statement (-tok parameter)|None|
|ttBufferSize  |Buffer Size for Temporary Tables (-Bt attribute)|None|
|msgBufferSize |Message buffer size (-Mm attribute)|None|
|compileUnderscore|COMPILE statement allows underscores (-zn parameter)|False|
|paramFile     |Parameter file (-pf parameter). -pf is always the first argument on the command line.|None|
|debugReady    |Port on which debugger should connect (disabled by default)|None|
|tempDir       |Temporary directory for Progress runtime (-T parameter)|None|
|assemblies    |.Net assemblies directory (-assemblies parameter). Attribute is skipped if file can't be found|None|
|quickRequest  |Quick request (-q parameter)|True|

† Only one of those attributes is mandatory
‡ Mandatory attribute

## Parameters as nested elements

### [DBConnection](PCTConnection.md) (or [PCTConnection](PCTConnection.md))

Adds a database connection on startup

### [[DBConnectionSet]]

Adds a group of database connection on startup

### [Propath](http://ant.apache.org/manual/using.html#path)

Creates a nested propath, and adds it to the implicit propath.

### [[Option]] (or [[PCTRunOption|Option]])

Adds an additional command line option to OpenEdge executable. These options are always appended at the end of the standard command line (before -p parameter).

_WARNING : an option containing a space will be surrounded by quotes. If a value is needed by a parameter, add it in the value attribute. This is needed if the value contains spaces for example._

### [[Parameter]]

Creates a parameter which can be read in the called procedure using `DYNAMIC-FUNCTION('getParameter' IN SOURCE-PROCEDURE, INPUT 'ParameterName')`. Returned value type is CHARACTER. If parameter is not defined, the function returns `?`. Duplicate keys are not allowed (first one in the list is used).

### [[OutputParameter]]

Adds a character `OUTPUT PARAMETER` to the called procedure. This value is then written to the specified Ant property.

### [[Profiler]]

Defines profiler options.

### [[DBAlias]]

Adds aliases on DB connection

### env

It is possible to specify environment variables to pass to the system command via nested `<env>` elements.

| **Attribute**| **Description**| **Default value**|
|:-------------|:---------------|:------------:|
|key †          |The name of the environment variable. _Note: (Since Ant 1.7) For Windows, the name is case-insensitive._|None|
|value †        |The literal value for the environment variable.|None|
|path          |The value for a PATH like environment variable. You can use ; or : as path separators and Ant will convert it to the platform's local conventions.|None|
|file          |The value for the environment variable. Will be replaced by the absolute filename of the file by Ant.|None|

† Only one of those attributes is mandatory
‡ Mandatory attribute

## About verbose attribute

The main procedure generated by PCT (calling your own procedure) always contains a shared variable definition :
```
DEFINE NEW SHARED VARIABLE pctVerbose AS LOGICAL NO-UNDO INITIAL True/False.
```
The main procedure will also display some information (such as propath, database connections, parameters) if verbose switch is on (-v or -d in the Ant command line).
In your own procedure, you can take advantage of this variable to display some information based on this verbose attribute :
```
DEFINE SHARED VARIABLE pctVerbose AS LOGICAL NO-UNDO.

IF pctVerbose THEN MESSAGE "Entering foo.p".
...
```

## Examples

### Example 1
```xml
<PCTRun procedure="test.p" />
```
Commandline : `$DLC/bin/_progres -b -p test.p`

### Example 2
```xml
<PCTRun procedure="test/test.p" graphicalMode="true" parameter="foobar" />
```
Commandline : `%DLC%/bin/prowin32 -b -param foobar -p test/test.p`

### Example 3
```xml
<pct:run procedure="test/test.p" graphicalMode="true" parameter="foobar">
  <DBConnection dbName="foo" dbDir="base" singleUser="true">
    <PCTAlias name="foo2" />
    <PCTAlias name="foo3" />
  </DBConnection>
  <DBAlias name="foo4" value="foo" />
  <propath>
    <pathelement path="src/include" />
    <pathelement path="src/include2" />
  </propath>
  <Option name="-cprcodeout" value="utf-8" />
  <Parameter name="Param1" value="Value1" />
  <Parameter name="Param2" value="Value2" />
  <OutputParameter name="FirstParam" />
  <OutputParameter name="SecondParam" />
</pct:run>
```
Commandline : `$DLC/bin/prowin32 -b -param foobar -cprcodeout utf-8 -p pctinitxxxx.p`

Procedure test/test.p could be:
```
 /* Two OutputParameter nodes */
 define output parameter param1 as character no-undo.
 define output parameter param2 as character no-undo.

 { myinclude.i } /* Will be found in src/include and src/include2 */

 find first foo.MyTable. /* As foo database is connected */
 find first foo2.MyTable. /* As foo2 is an alias */
 find first foo3.MyTable. /* As foo3 is also an alias */

 define variable myvar as char no-undo.
 assign myvar = dynamic-function('getParameter' in source-procedure, 'Param1').
 display myvar. /* will display Value1 */

 assign param1 = foo.MyTable.Field1.
 assign param2 = foo.MyTable.Field2.

 if (somecondition) then
   return '0'. /* Don't forget to return a value */
 else
   return '20'. /* Any non-zero value is an error */
```

After PCTRun task execution, Ant properties FirstParam and SecondParam can be accessed with `${FirstParam}` and `${SecondParam}`, e.g.
```xml
 <echo message="FirstParam is ${FirstParam} and SecondParam is ${SecondParam}" />
```
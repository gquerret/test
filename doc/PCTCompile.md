## Description

Compile OpenEdge procedures and classes.

## XML namespace

`<pct:compile />`

### Parameters

| **Attribute**| **Description**| **Default value**|
|:-------------|:---------------|:---------------:|
|destDir  |Directory where to put compiled code|None|
|stopOnError   |If set to true, stop compilation as soon as an error occurs.|False|
|numThreads    |Starts n parallel compilation threads. Don't use multiple threads when compiling classes.|1|
|multiCompile  |Change `COMPILER:MULTI-COMPILE` attribute. |False|
|minSize       |Boolean value of `MIN-SIZE` option.|False|
|MD5           |Boolean value of `GENERATE-MD5` option.|False|
|streamIO      |Boolean value of `STREAM-IO` option.|False|
|v6Frame       |Boolean value of `V6FRAME` option. |False|
|useUnderline  | `USE-UNDERLINE` option of `V6FRAME` |False|
|useRevVideo   | `USE-REVVIDEO` option of `V6FRAME` |False|
|runList       |True to generate a `.run` file for each compiled file, which summarizes RUN statements|False|
|listing       |Boolean value of `LISTING` option. Generated file name is identical to source file name, and is stored in `xrefDir`|False|
|listingSource |Generates listing file from preprocessed source code (value `preprocessor`) or from standard source code (empty value or not defined).|False|
|preprocess    |Boolean value of `PREPROCESS`attribute. Generated file name appends .preprocess to source file name, and is stored in `preprocessDir`.|False|
|preprocessDir |Target directory where preprocessed files are written.|`<destDir>/.pct` |
|debugListing  |Boolean value of `DEBUG-LIST` option. Generated file name appends .dbg to file name, and is stored in `debugListingDir`.|False|
|debugListingDir|Target directory where debug listing files are written. |`destDir/.pct`|
|flattenDebugListing|Flattens directory structure for debug listing files|True|
|stringXref    |Boolean value of `STRING-XREF`option. Generated file name appends .strxref to source file name. |False|
|appendStringXref|Appends `STRING-XREF` to a single file. |False|
|keepXref      |Keeps the generated XREF file for each file. Generated file name replaces extension of source file name with `.xref`. |False|
|noParse       |Always recompile, and skip XREF generation as well as .crc and .inc files. |False|
|xrefDir       |Target directory where PCT files (CRC, includes, preprocess, listing) will be created. |`<destDir>/.pct`|
|xmlXref       |Generates XREF in XML format.|False.|
|forceCompile  |Always compile everything.|False.|
|xcode         |Compiles using XCODE option. Disables XREF and LISTING options.|False.|
|xcodeKey      |Sets specific key for encrypted procedures. _Deprecated: use XCodeSessionKey attribute in PCTRun_ |None|
|languages     |Comma-separated list of language segments to include in the compiled r-code. `LANGUAGES` option of the COMPILE statement|None|
|textGrowth    |`TEXT-SEG-GROWTH` option of the COMPILE statement.|None|
|relativePaths |Use relative paths instead of absolute paths for propath and filesets. Every fileset dir has to be in propath. |False|
|progPerc      |Show progression percentage every `x` percent.|0 (not displayed)|
|displayFiles | 1 will display files to be recompiled (and reason). 2 will display all files. 0 doesn't display anything |0 (no display)|
|requireFullKeywords | Strict-mode compiler option (11.7+). Output redirected to `.warnings` files in `.pct` directory|False|
|requireFullNames | Strict-mode compiler option (11.7+). Output redirected to `.warnings` files in `.pct` directory|False|
|requireFieldQualifiers | Strict-mode compiler option (11.7+). Output redirected to `.warnings` files in `.pct` directory|False|
|requireReturnValues | Strict-mode compiler option (12.2+). Output redirected to `.warnings` files in `.pct` directory|False|
|outputType | `json` will display the errors and warnings of source files in `<destDir>/.pct/project-result.json`. |None|
|callbackClass | Callback class (implementation of rssw.pct.AbstractCompileCallback) | None |

† Only one of those attributes is mandatory
‡ Mandatory attribute

PCTCompile inherits attributes from [[PCT]] and [[PCTRun]].

## Parameters as nested elements

### [Resource Collection](http://ant.apache.org/manual/Types/resources.html#collection)

Files to be compiled

### [Mapper](http://ant.apache.org/manual/Types/mapper.html)

Adds a custom mapper

## Examples

#### Example 1

```xml
<PCTCompile destDir="build" dlcHome="${env.DLC}">
  <fileset dir="src">
    <include name="**/*.p"/>
    <exclude name="test/**"/>
  </fileset>
  <propath>
    <pathelement path="src/include"/>
  </propath>
</PCTCompile>
```
Compiles every .p in src directory (and subdirs) except those from src/test, with PROPATH set to src/include, and put .r in build directory.

#### Example 2

```xml
<PCTCompile destDir="build" dlcHome="${DLC}" relativePaths="true">
  <fileset dir="custom" />
  <fileset dir="main">
    <present present="srconly" targetdir="custom" />
  </fileset>
  <propath>
    <pathelement location="custom" />
    <pathelement location="main" />
  </propath>
</PCTCompile>
```
Compiles every file in custom and main directory, but skipping files in main where a file with same name is present in custom. Documentation on `<present>` selector can be found [here](http://ant.apache.org/manual/Types/selectors.html#presentselect).


#### Relative paths example

Consider the following file in src/foo/bar/test.p :
```
MESSAGE '{&FILE-NAME}' { foo/test.i }.
```
With the following include inc/foo/test.i :
```
'{&FILE-NAME}'
```
And this build file :
```xml
<path id="compilation.propath">
  <pathelement path="src;inc" />
</path>
<PCTCompile destDir="build1" dlcHome="${DLC}" relativePaths="false">
  <fileset dir="src" includes="**/*.p" />
  <propath refid="compilation.propath" />
</PCTCompile>
<PCTCompile destDir="build1" dlcHome="${DLC}" relativePaths="true">
  <fileset dir="src" includes="**/*.p" />
  <propath refid="compilation.propath" />
</PCTCompile>
```
If you execute build1/foo/bar/test.r and then build2/foo/bar/test.r, you'll see :
```
# Using relativePaths=false
/absolute/path/to/src/foo/bar/test.p /absolute/path/to/inc/foo/test.i
# Using relativePaths=true
src/foo/bar/test.p inc/foo/test.i
```
With relativePaths=false, if you compile the same code in two different directories, you end up with different rcode (CRC and MD5 won't match).
This can also be a problem when using TranMan : it's database contains either absolute or relative paths to file names, and if you have a different name,
TranMan won't find the translation.

#### Example 4

```xml
<typedef resource="types.properties" />
<PCTCompile destDir="build" dlcHome="${env.DLC}">
  <fileset dir="src">
    <include name="**/*.p"/>
    <exclude name="test/**"/>
  </fileset>
  <propath>
    <pathelement path="src/include"/>
  </propath>
  <chainedmapper>
    <flattenmapper />
    <rcodemapper /> <!-- Don't forget typedef declaration -->
  </chainedmapper>
</PCTCompile>
```
Compiles every .p in src directory (and subdirs) except those from src/test, with PROPATH set to src/include, and put .r in build directory (removing any subdirectory reference), i.e. ```src/foo/bar.p``` results in ```build/bar.r```

#### Example 5

```xml
<PCTCompile destDir="build" dlcHome="${env.DLC}">
  <fileset dir="src" includes="**/*.p" />
  <compositemapper>
    <regexpmapper from="^(.*)\.p$$" to="\1renamed.r" />
    <regexpmapper from="^(.*)\.t$$" to="triggers/\1.r" />
  </compositemapper>
</PCTCompile>
```
Compiles every .p in src directory (and subdirs), and apply a regexp for resulting file : any .p file results in a .r file appended with renamed, and any .t file results in .r file compiled in triggers directory.

#### Example 6

```xml
<PCTCompile numThreads="4" destDir="build" dlcHome="${env.DLC}">
  <fileset dir="src" includes="**/*.p,**/*.w" />
  <DBConnection dbName="sports" dbDir="target/db" readOnly="true" />
</PCTCompile>
```
Compiles every .p and .w in src directory (and subdirs), with 4 compilation threads, connected to sports database in read-only mode (no need for a database broker).
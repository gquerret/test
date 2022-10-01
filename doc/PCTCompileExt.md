⚠️ This page is not relevant anymore. Please use [[PCTCompile]] documentation.

## Description

This task is a rewrite of [[PCTCompile]] ; the only difference is this task is using a background Progress session, and the Java part controls the compilation. This allows more things : one example could be using custom mappers (see examples).

**Warning : there are some discrepancies between the original PCTCompile task and this one ; if you encounter a bug, please first test using PCTCompile before opening an issue. Bugs in PCTCompile are always considered first.**

## XML namespace

`<pct:compile_ext />`

## Parameters

| **Attribute**| **Description**|
|:-------------|:---------------|
|numThreads    |Starts n parallel compilation threads. Default value is 1.|Integer  |Optional        |1                 |
|destDir ‡ |Directory where to put compiled code|File     |Required        |No default value  |
|minSize       |Compile using option MIN-SIZE=`<value>`|Boolean  |Optional        |False             |
|MD5           |Compile using option GENERATE-MD5=`<value>`|Boolean  |Optional        |False             |
|streamIO      |Compile using option STREAM-IO=`<value>`|Boolean  |Optional        |False             |
|v6Frame       |Compile using option V6FRAME=`<value>`|Boolean  |Optional        |False             |
|runList       |Generates a .run file for each compiled file, which summarizes RUN statements|Boolean  |Optional        |False             |
|Listing       |Generates a listing file for each compiled file (LISTING attribute of COMPILE statement). Generated file name is identical to source file name.|Boolean  |Optional        |False             |
|Preprocess    |Generates a preprocessed file for each compiled file (PREPROCESS attribute of COMPILE statement). Generated file name appends .preprocess to source file name.|Boolean  |Optional        |False             |
|preprocessDir |Target directory where preprocessed files are written|File     |Optional        | `<destDir>/.pct` |
|DebugListing  |Generates a debug-listing file for each compiled file (DEBUG-LIST attribute of COMPILE statement). Generated file name appends .dbg to file name|Boolean  |Optional        |False             |
|debugListingDir|Target directory where debug listing files are written|File     |Optional        | `<destDir>/.pct` |
|keepXref      |Keeps the generated XREF file for each file. Generated file name replaces extension of source file name with .xref|Boolean  |Optional        |False             |
|failOnError   |If task should end just after a failed file compilation|Boolean  |Optional        |True              |
| ~~noXRef~~   | ~~Don't use XREF when compiling or when reading files to compile~~ | ~~Boolean~~ | ~~Optional~~   | ~~False~~        |
|noParse       |Always recompile, and skip XREF generation as well as .crc and .inc files|Boolean  |Optional        |False             |
|XRefDir       |Where PCT files (CRC, includes, preprocess, listing and debug-listing) should be created|File     |Optional        | `<destDir>/.pct` |
|forceCompile  |Always compile everything|Boolean  |Optional        |False             |
|XCode         |Compiles using XCODE option|Boolean  |Optional        |False             |
|XCodeKey      |Sets specific key for encrypted procedures|String   |Optional        |No default value  |
|noCompile     |Just prints files to recompile with the reason why, without executing COMPILE statement|Boolean  |Optional        |False             |
|Languages     |Identifies which language segments to include in the compiled r-code. LANGUAGES option of the COMPILE statement|String   |Optional        |No default value  |
|textGrowth    |TEXT-SEG-GROWTH option of the COMPILE statement|Integer  |Optional        |No default value  |
|multiCompile  |Set COMPILER:MULTI-COMPILE attribute|Boolean  |Optional        |False             |
|relativePaths |Use relative paths instead of absolute paths for propath and filesets|Boolean  |Optional        |False             |
† Only one of those attributes is mandatory ‡ Mandatory attribute

PCTCompile inherits attributes from [[PCT]] and [[PCTRun]].

## Parameters as nested elements

### [Fileset](http://ant.apache.org/manual/Types/fileset.html)

Adds a file set to the file list to compile

### [Mapper](http://ant.apache.org/manual/Types/mapper.html)

Adds a custom mapper

## Examples
```xml
<PCTCompileExt destDir="build" dlcHome="${env.DLC}">
  <fileset dir="src">
    <include name="**/*.p"/>
    <exclude name="test/**"/>
  </fileset>
  <propath>
    <pathelement path="src/include"/>
  </propath>
  <mapper type="flatten" />
</PCTCompileExt>
```
Compiles every .p in src directory (and subdirs) except those from src/test, with PROPATH set to src/include, and put .r in build directory (removing any subdirectory reference), i.e. ```src/foo/bar.p``` results in ```build/bar.r```

```xml
<PCTCompileExt destDir="build" dlcHome="${env.DLC}">
  <fileset dir="src">
    <include name="**/*.p"/>
  </fileset>
  <compositemapper>
    <regexpmapper from="^(.*)\.p$$" to="\1renamed.r" />
    <regexpmapper from="^(.*)\.t$$" to="triggers/\1.r" />
  </compositemapper>
</PCTCompileExt>
```
Compiles every .p in src directory (and subdirs), and apply a regexp for resulting file : any .p file results in a .r file appended with renamed, and any .t file results in .r file compiled in triggers directory.

```xml
<PCTCompileExt numThreads="3" destDir="build" dlcHome="${env.DLC}">
  <fileset dir="src">
    <include name="**/*.p"/>
    <include name="**/*.w"/>
  </fileset>
</PCTCompileExt>
```
Compiles every .p and .w in src directory (and subdirs), with 3 compilation threads.
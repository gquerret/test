## Description

Create OpenEdge procedure library (.pl)

## XML Namespace

`<pct:library />`

## Parameters

| **Attribute**| **Description**| **Default value**|
|:-------------|:---------------|:--------:|
|destFile †    |R-code library to create|None|
|sharedFile †  |Memory mapped library to create|None|
|encoding      |Character encoding used to store filenames.|None|
|noCompress    |Disable library compression.|False (i.e. compression enabled)|
|cpInternal    |Internal code page (-cpinternal parameter)|None|
|cpStream      |Stream code page (-cpstream parameter)|None|
|cpColl        |Collation table (-cpcoll parameter)|None|
|cpCase        |Case table (-cpcase parameter)|None|
|basedir       |The directory from which to store the files.|None|
|includes      |Comma- or space-separated list of patterns of files that must be included. All files are included when omitted.|None|
|includesFile  |The name of a file. Each line of this file is taken to be an include pattern.|None|
|excludes      |Comma- or space-separated list of patterns of files that must be excluded. No files (except default excludes) are excluded when omitted.|None|
|excludesFile  |The name of a file. Each line of this file is taken to be an exclude pattern.|None|
|defaultExcludes|Indicates whether default excludes should be used or not ("yes"/"no"). Default excludes are used when omitted.|True|

† Only one of those attributes is mandatory ‡ Mandatory attribute

PCTLibrary inherits attributes from [[PCT]].

## Parameters as nested elements

### fileset

Adds a file set to the library

## Examples

```xml
<PCTLibrary destfile="${dist}/mylib.pl" basedir="${build}" />
```
stores all files in the ${build} directory into a file called mylib.pl in the ${dist} directory.

```xml
<PCTLibrary destfile="${dist}/mylib.pl" basedir="${build}" includes="**/*.r" excludes="test/*" />
```
stores all .r files in the ${build} directory (and subdirectories) except from the files in the test subdirectory, into a file called mylib.pl in the ${dist} directory.

```xml
<PCTLibrary destfile="${dist}/mylib.pl">
  <fileset dir="${build}">
    <include name="**/*.r" />
    <exclude name="test/*" />
  </fileset>
</PCTLibrary>
```
is similar to the previous example, but using nested fileset.
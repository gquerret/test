## Description

Converts Webspeed HTML files to .w

## XML namespace

`<pct:webspeed />`

## Parameters

| **Attribute**| **Description**|**Default value**|
|:-------------|:---------------|:---------------:|
|destDir ‡ |Directory where to put .w files|None|
|failOnError   |If task should end after a failed file transformation.|False|
|forceCompile  |Always rebuild every HTML file. |False|
|debug         |Adds `debug` to `e4gl-gen.p` options. |False|
|keepMetaContentType|Adds `keep-meta-content-type` to `e4gl-gen.p` options. |False|
|webObject     |Adds `web-object` to `e4gl-gen.p` options. If false, adds include option. |True|

† Only one of those attributes is mandatory ‡ Mandatory attribute

PCTWSComp inherits attributes from [[PCT]] and [[PCTRun]].

## Parameters as nested elements

### [Fileset](http://ant.apache.org/manual/Types/fileset.html)

Adds a file set to the file list to compile

## Examples
```xml
<PCTWSComp destDir="build">
  <fileset dir="." includes="test.html" />
</PCTWSComp>
```
Converts test.html and put test.w in build directory.
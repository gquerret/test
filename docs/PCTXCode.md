## Description

This task encrypts procedures and include files using the Progress xcode utility.

## XML Namespace

`<pct:xcode />`

## Parameters

| **Attribute**| **Description**| **Default value**|
|:-------------|:---------------|:--------:|
|destDir ‡     |Where encrypted files should be dropped|None|
|key           |Encryption key (-k argument)|Default key|
|lowercase     |If files should be converted to lowercase before encryption (-l argument)|False             |
|overwrite     |Always overwrite files|False             |

† Only one of those attributes is mandatory ‡ Mandatory attribute

## Parameters as nested elements

### [Fileset](http://ant.apache.org/manual/Types/fileset.html)

Adds a file set to the file list to encrypt

## Examples

```xml
<PCTXCode destDir="xbuild" key="mykey">
  <fileset dir="." includes="*.p" />
</PCTXCode>
```
Encrypt every .p file in current directory using mykey `key`, and drop files in xbuild directory.
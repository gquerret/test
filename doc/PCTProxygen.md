## Description

Generate proxies based on PXG/XPXG files

## XML namespace

`<pct:proxygen />`

## Parameters

| **Attribute**| **Description**| **Default value**|
|:-------------|:---------------|:--------:|
|srcFile ‡     |PXG or XPXG file to use|No default value  |
|keepFiles     |Leave proxy files|False               |
|workingDirectory ‡|Working directory|Project's basedir|

† Only one of those attributes is mandatory
‡ Mandatory attribute

## Parameters as nested elements

### [jvmarg](http://ant.apache.org/manual/using.html#arg)

Use nested `<jvmarg>` elements to specify arguments for the forked VM.

### [Resource Collection](http://ant.apache.org/manual/Types/resources.html)

List of PXG files to be processed

## Examples
```xml
<!-- xpxg files may contain absolute paths. xmltask is really useful in this case -->
<xmltask source="proxy.xpxg" dest="proxy2.xpxg">
  <replace path="/:WSAD/:AppObject/:PGGenInfo/:WorkDir/text()" withText="build-proxygen\" />
  <!-- There may be other nodes to transform -->
</xmltask>
<PCTProxygen srcFile="proxy2.xpxg" workingDirectory="." />
```
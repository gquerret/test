## Description

Generates XML documentation from OpenEdge classes. An example of generated documentation is available [here](http://riverside-software.fr/pct/OpenEdge.DataAdmin.Binding.DataAdminContext.xml) (full documentation for OpenEdge.DataAdmin package is available [here](http://riverside-software.fr/pct/class_documentation.zip)).

Comments have to be written using a specific syntax to be parsed correctly; documentation is [here](StandardCommentBlock).

## XML namespace

`<pct:classdocumentation />`

## Requirements

### 11.5 to 11.7, 12.0

This task requires JAR files ast.jar and ast-dependencies.jar in your classpath. You can find them:
* In `%DLC%\java\ant-libs` (OpenEdge 11.7 and 12.0)
* In `%DLC%\oeide\eclipse\plugins\com.progress.openedge.pdt.abldoc.core_11.5.1.00\lib` (OpenEdge 11.5 and 11.6). You'll need a Progress Developer Studio licence to have those files installed.

Drop the JAR files in `${ANT_HOME}/lib` or call Ant with `-lib /path/to/ast.jar -lib /path/to/ast-dependencies.jar`.

Task isn't declared in the same .properties file as the other tasks. You'll need to add this line to your build.xml :
```
  <taskdef resource="extras115.properties" />
```
PCT build #200 (or above) is required for extras115.properties

### Up to 11.3

**This method is available for legacy purpose, and is not maintained anymore**

> This task requires JAR file oe\_common\_services.jar in your classpath. This JAR file is located **inside** `%DLC%\oeide\Architect_repo\plugins\com.openedge.pdt.core_XXX.jar` (for 11.1, it may be a different path for previous versions). Remember that JAR files are in fact ZIP files, so use an appropriate tool to extract the content. You'll need an OpenEdge Architect licence to have those files installed.
> Please note the following requirement :
>  * PCT 178 requires oe\_common\_services from 11.1
>  * PCT 179+ requires oe\_common\_services from 11.2 or 11.3
>  * PCT 188+ requires oe\_common\_services from 11.3.2 (not tested with previous versions)
>  * No support for ClassDocumentation in PCT below 178
>
>Drop the JAR file in `${ANT_HOME}/lib` or call Ant with `-lib /path/to/oe_common_services.jar`. Please note that oe\_common\_services.jar from 11.4 is not supported yet.
>
>Task isn't declared in the same .properties file as the other tasks. You'll need to add this line to your build.xml :
```
  <taskdef resource="extras.properties" />
```
_Important note : as of build #200, [parser.jar](https://github.com/Riverside-Software/pct/raw/master/lib/parser.jar) also has to be present in classpath (same way as oe\_common\_services.jar)_

### Using 11.4

Version not supported

## Preprocessing

It's recommended to generate documentation from preprocessed source. Use preprocessDir attribute of PCTCompile task to generate preprocessed classes, then use ClassDocumentation on this directory.

### Parameters

| **Attribute**| **Description**| **Default value**|
|:-------------|:---------------|:---------------:|
|destDir ‡     |Directory where to put XML files|No default value  |
|encoding      |Use specified encoding when reading source files. Not yet implemented|No default value  |

† Only one of those attributes is mandatory
‡ Mandatory attribute

ClassDocumentation inherits attributes from [[PCT]].

## Parameters as nested elements

### fileset

Adds a file set

## Examples

```xml
<PCTCompile destDir="build" preprocessDir="preprocess" dlcHome="${DLC}">
  <fileset dir="src" includes="**/*.cls" />
  <propath path="src" />
</PCTCompile>
<ClassDocumentation destDir="doc" dlcHome="${DLC}">
  <fileset dir="preprocess" includes="**/*.cls" />
  <propath path="preprocess" />
</ClassDocumentation>
```

Compiles every .cls in src directory (and subdirs) in build directory, generates preprocessed classes in preprocess directory, then generate XML documentation from the preprocessed classes.
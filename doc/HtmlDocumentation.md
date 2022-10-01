## Description

Generates HTML documentation from output of [[ClassDocumentation]] task. A small example of generated documentation is available [here](http://riverside-software.fr/pct/documentation/index.html), a larger one [there](http://help.consultingwerkcloud.com/smartcomponent_library/release/).

Documentation on the overall process can be found [here](http://riverside-software.fr/files/SmartDox_PUG_Challenge.pdf).

Documentation templates are included in PCT. If you want to use your own templates, you have to specify the templateDir attribute. Documentation on templates is located [here](TemplatesDescription).

## XML namespace

`<pct:htmldocumentation />`

## Requirements

This task only works under Windows environment, and is not compatible with OpenEdge 10. The task isn't declared in the same .properties file as the other tasks. You'll need to add this line to your build.xml :
```
  <taskdef resource="extras115.properties" />
```

### Parameters

| **Attribute**| **Description**| **Default value**|
|:-------------|:---------------|:---------------:|
|sourceDir ‡   |Directory where XML files are located|No default value  |
|destDir ‡     |Directory where HTML filesare written|No default value  |
|title         |HTML document title|Class reference   |
|templateDir   |Directory where templates are located. If this attribute is not set, default templates are used.|No default value  |
|services      |Path to services.xml file to customize code documentation generator.|No default value  |
|treeViewOverview|Generates classes treeview|True              |
|preloadClasses|Preload classes |True              |

† Only one of those attributes is mandatory
‡ Mandatory attribute

HTMLDocumentation inherits attributes from [[PCT]].

## Parameters as nested elements

None

## Bugs

This task is work in progress, so please [report](https://github.com/Riverside-Software/pct/issues) any issue.

## Examples

```xml
<PCTCompile destDir="build" preprocessDir="preprocess" dlcHome="${env.DLC}">
  <fileset dir="src">
    <include name="**/*.cls"/>
  </fileset>
  <propath>
    <pathelement path="src"/>
  </propath>
</PCTCompile>
<ClassDocumentation destDir="doc" dlcHome="${env.DLC}">
  <fileset dir="preprocess" includes="**/*.cls" />
</ClassDocumentation>
<HTMLDocumentation sourceDir="doc" destDir="html" dlcHome="${env.DLC}" />
```

Compiles every .cls in src directory (and subdirs) in build directory, generates preprocessed classes in preprocess directory, then generates XML documentation from the preprocessed classes, and then generates HTML documentation from XML files, using predefined templates.
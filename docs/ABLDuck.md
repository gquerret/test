## Description

Generates documentation from OpenEdge classes (currently, plans to support procedures). ABLDuck is based of the JSDuck documentation tool for JavaScript.

### Features
* JavaDoc style comments
* Markdown support
* Globally searchable on class name, method name, property name and event name
* Syntax highlighted code examples in the comment
* Tag support: {@link}, @author, @internal, @deprecated, @param and @return
* View class menu by package or inheritance
* Automatic linking of known datatypes
* Print support

## Requirements

Please see the [ClassDocumentation](https://github.com/Riverside-Software/pct/wiki/ClassDocumentation) task documentation for requirements as these are identical.

If you would like to use the print button, please make sure to serve the index.php file and not the index.html file.

## Preprocessing

It's recommended to generate documentation from preprocessed source. Use preprocessDir attribute of PCTCompile task to generate preprocessed classes, then use ClassDocumentation on this directory.

## Usage

Comments have to be written using a specific syntax to be parsed correctly, if you are already familiar with the JavaDoc style you will recognize it immediately. 

You can test how your comment will render using [this](https://spazzymoto.github.io/ablduck/). __Note:__ this is not an exact representation although it is quite close.

    /**
     * Comment line 1
     * Comment line 2
     * 
     *     DEFINE VARIABLE cTest   AS CHARACTER  NO-UNDO. /* Code example */
     *
     * @author John Doe
     etc
     */

It is important to start your comment with `/**` and end it with `*/` ; please note that anything else on this line will be trimmed off.

## Tag Usage

### {@link} 
You can use the link tag to link to any other class in your preprocessed codebase.  

```
  {@link  class  (linkText optional)}  
  {@link  class-method-methodName (linkText optional)}  
  {@link  class-property-PropertyName (linkText optional)}  
  {@link  class-event-EventName (linkText optional)}  
```

### @author
Any text following the @author tag will be substituted into the Author placeholder in the documentation.  

```
@author John Doe
```

### @internal
This tag takes no arguments. If you put this tag in a comment it will add a line to the top of the items comment saying that this item is for internal use only and that you should not rely on its existence.  
```
@internal
```

### @deprecated
This tag takes 2 arguments, a version number first and some text after. The text can be used to link to the new class, method or property etc.  
```
   @deprecated 0.0.1 Please use {@link  class  (linkText optional)} instead.  
```

### @param
This tag can be used to comment input/output parameters for a method, constructor or event. Markdown will also be applied to these comments.  
```
@param This would be some text in the parameters comment section.
```

### @return
This tag can be used like the @param tag to specify a comment for the return parameter.  
```
@return This would be some text in the return parameters comment section.
```

### Markdown support
For more information on what is available with the markdown support please visit [http://commonmark.org/](http://commonmark.org/)

### Parameters

| **Attribute**| **Description**| **Default value**|
|:-------------|:---------------|:---------------:|
|destDir ‡     |Directory where to put files|No default value  |
|encoding      |Character encoding|Platform default value|
|title         |Title to use for the documentation|ABLDuck documentation  |

† Only one of those attributes is mandatory
‡ Mandatory attribute

ABLDuck inherits attributes from [[PCT]].

## Parameters as nested elements

### fileset

Adds a file set

## Examples

```xml
<PCTCompile destDir="build" preprocessDir="preprocess" dlcHome="${DLC}">
  <fileset dir="src" includes="**/*.cls" />
  <propath path="src" />
</PCTCompile>
<ABLDuck destDir="doc" dlcHome="${DLC}" title="My Documentation">
  <fileset dir="preprocess" includes="**/*.cls" />
  <propath path="preprocess" />
</ABLDuck>
```

Compiles every .cls in src directory (and subdirs) in build directory, generates preprocessed classes in preprocess directory, then generate documentation from the preprocessed classes.
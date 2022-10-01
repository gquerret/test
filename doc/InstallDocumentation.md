# Installation

## System requirements

The PCT plug-in requires Ant 1.9 or higher, and has only been tested with 1.10 version of Ant. To obtain more information about this wonderful build tool, visit the [official Ant home page](http://ant.apache.org).

PCT binaries can be used with version 11 and 12 of OpenEdge. Compatibility with version 8 and 9 has been dropped in 2016 (in commit 109e453). Support for version 10 has been dropped in 2019 (version 213). It is still technically possible to execute PCT with OpenEdge 10, but without warranty of any kind (and no support will be provided).

## Installation (binary package)

The PCT plug-in comes as a single .jar file. Before you can use the PCT tasks in your build scripts, you have to add them to your system. The simplest way to install PCT is to copy the JAR file into the `$ANT_HOME/lib` directory. In this case, you just have to declare the tasks in your build script as follows :
```xml
<taskdef resource="PCT.properties" />
<typedef resource="types.properties" />
<!-- Next line only for tasks using OpenEdge parser, see ClassDocumentation task -->
<typedef resource="extras.properties" />
```
You can also use the `-lib` attribute in the command line if you don't want to copy PCT.jar in `$ANT_HOME/lib`.

You can call Ant with `-DPCT-SRC=true` to force PCT to work with its source code instead of the compiled version.
```
ant -DPCT-SRC=true your_target_name
```
When working with source code, you'll need a working OpenEdge development license with development tools and include files.

PCT tasks can be used with XML namespaces. Check Antlib namespaces before using that. One way to use PCT this way is to declare the pct namespace in your project :
```xml
<project xmlns:pct="antlib:eu/rssw/pct" xmlns:extras="antlib:eu/rssw/pct/oedoc">
  <!-- Next two lines only if PCT.jar doesn't live in $ANT_HOME/lib -->
  <taskdef uri="antlib:eu/rssw/pct" resource="eu/rssw/pct/antlib.xml" />
  <taskdef uri="antlib:eu/rssw/pct/oedoc" resource="eu/rssw/pct/oedoc/antlib.xml" />
...
</project>
```
After having declared PCT, you'll be able to use PCT tasks in this manner :
```xml
  <pct:run procedure="..." />
  <pct:compile ... /> 
```
Documentation shows "old" names first, followed by the name in the pct namespace.

Please note that the behavior of PCT remains unchanged whichever style you're choosing. Old names are not deprecated, and will live a long life...
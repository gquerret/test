## Pointy bracket hell? ant-contrib hell?

Despite being primarily a build tool, Apache Ant is a very practical tool for manipulating files including zip files, copy, resource processing, …​ But if ever you’ve been working with a build.xml file and found yourself a little restricted by all those pointy brackets, or found it a bit weird using XML as a scripting language and wanted something a little cleaner and more straight forward, then maybe Ant scripting with [Groovy](http://groovy-lang.org) might be what you’re after.

## Hmm, Groovy... But what is Groovy?

[Wikipedia](https://en.wikipedia.org/wiki/Groovy_(programming_language)) explains it:
> Apache Groovy is an object-oriented programming language for the Java platform. It is a dynamic language with features similar to those of Python, Ruby, Perl, and Smalltalk. It can be used as a scripting language for the Java Platform, is dynamically compiled to Java virtual machine (JVM) bytecode, and interoperates with other Java code and libraries. Groovy uses a Java-like curly-bracket syntax. Most Java code is also syntactically valid Groovy, although semantics may be different.

## How easy is it?

[This page](http://groovy-lang.org/scripting-ant.html) is a very good introduction to Ant scripting in Groovy.

A short example on how to execute an OpenEdge procedure in Groovy:
```groovy
def ant = new AntBuilder()          
ant.taskdef (resource: 'PCT.properties')

ant.PCTRun(procedure: 'updateCustomers.p', dlcHome: '/usr/dlc') {
  DBConnection(dbName: 'sports2000', dbDir: '/db/prod')
}
```

Another example on how to execute the same procedure on each OpenEdge database in a directory:
```groovy
new File('databases').traverse(type: FileType.FILES, nameFilter: ~/[a-z]+\.db/) { db ->
  ant.PCTRun(procedure: 'updateCustomers.p', dlcHome: '/usr/dlc') {
    DBConnection(dbName: db.name, dbDir: db.parent)
  }
}
```

## I don't want new dependencies!

If you're working with PCT, it's because your product is written in OpenEdge. OpenEdge includes a Java Virtual Machine since ages. Groovy is pure Java. PCT is pure Java. Both are just a JAR files. This means that if you want to use Groovy / PCT to deploy on customer site, you can rely on the JVM bundled with OpenEdge, which is available at `$DLC/jre`. So once the `DLC` variable is correctly set, you can execute your update script:
```
$DLC/jre/bin/java -jar groovy-pct.jar update-script.groovy
```

## What can I use it for?

* Rolling out new release
* Database update mechanism
* ...

## Examples

### Use command-line parameters

```groovy
def cli = new groovy.util.CliBuilder(usage: 'java -jar groovy-pct.jar script.groovy [options]')
cli.dlc(args: 1, 'OpenEdge installation directory')
cli.host(args: 1,optionalArg: true, 'Hostname')
cli.port(args: 1,optionalArg: true, 'Port')
cli.user(args: 1,optionalArg: true, 'User name')
cli.password(args: 1,optionalArg: true, 'Password')

def options = cli.parse(args)
```

### Read info from database

```groovy
propath = [ 'dir1', 'dir2', 'dir3']
ant.PCTRun (procedure: 'readinfo.p', dlcHome: System.env['DLC']) {
  DBConnection (dbname: 'dbname', dbdir: '/db/db1')
  Propath {
    propath.each { pathelement (location: it) }
  }
  OutputParameter (name: 'xxx')
  OutputParameter (name: 'yyy')
}
println "-> Output parameters : '${ant.project.properties.xxx}' and '${ant.project.properties.yyy}'"
```

With this OpenEdge procedure:
```openedge
define output parameter op1 as character no-undo.
define output parameter op2 as character no-undo.
assign op1 = 'Your logic here'.
assign op2 = 'Your logic here'.
return '0'.
```

### Execute updates without a compilation license

Make sure all procedures are xcode'd (hint: use [[PCTXCode]]). Then use xCodeInit attribute in PCTRun to xcode init procedure on the fly. You have to make sure the `xcode` executable is available in the PATH. 
```groovy
ant.PCTRun (procedure: 'readinfo-xcode.p', dlcHome: options.dlc, xCodeInit: true)
```

### XMLNS style

```groovy
def ant = new AntBuilder()
ant.taskdef(uri:'antlib:eu.rssw.pct', resource:'eu/rssw/pct/antlib.xml')
def pct = groovy.xml.NamespaceBuilder.newInstance(ant, 'antlib:eu.rssw.pct')
pct.run(procedure: 'rssw.p', dlcHome: System.env['DLC'])
```

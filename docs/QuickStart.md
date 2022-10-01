# Quick start

## Step 1 : first build.xml file (aka Hello, world!)

Let's assume Ant and PCT are correctly installed (see [[InstallDocumentation]]). We'll create a new Progress project in a directory called MyProject. As a good practice, we'll separate sources from build files : sources will be stored in `src/oe` directory, and build output in `target/oe` directory.

We'll now create one or more procedures in the src/oe subdir. For example, in `MyProject/src/oe/test.p`:
```
MESSAGE "This is a test file".
```

And now, in MyProject/build.xml :
```xml
<?xml version="1.0" encoding="utf-8"?>
<project name="MyProject">
 <property environment="env" />
 <taskdef resource="PCT.properties" />
 <typedef resource="types.properties" />

 <target name="build" description="Builds source files">
  <mkdir dir="target/oe" />
  <PCTCompile destDir="target/oe" dlcHome="${env.DLC}">
   <fileset dir="src/oe" includes="*.p" />
  </PCTCompile>
 </target>
</project>
```

Open ProEnv (in order to have the DLC variable correctly set). Ant also assumes that `ANT_HOME`, `JAVA_HOME` are defined, but that's part of Ant installation. Then cd to the MyProject directory, and then type `ant build`. You should get the following :
```
Buildfile: build.xml

build:
    [mkdir] Created dir: /home/justus/MyProject/target/oe
[PCTCompile] PCTCompile - Progress Code Compiler
[PCTCompile] 1 file(s) compiled

BUILD SUCCESSFUL
Total time: 1 seconds
```
And you should have a subdir called target/oe, containing a test.r file.

A few words on this :
* Line 4 tells Ant to load environment variables so that they could be accessed with ${env.VARIABLE\_NAME} : useful for DLC...
* Line 6 tells Ant to load the mapping between tasks name (e.g. PCTCompile) and Java class files: this is mandatory to have a working PCT.
* Lines 10 to 14 tells PCT to compile every .p file in the src/oe directory, and then put them in the destDir directory.

## Step 2 : adding a database

We'll create a subdir called db, containing the database dump file (called db.df). Just create this file :
```
ADD TABLE "MyTable"
  AREA "Schema Area"
  DUMP-NAME "MyTable"

ADD FIELD "Fld1" OF "MyTable" AS character 

ADD FIELD "Fld2" OF "MyTable" AS character 

ADD INDEX "MyTable-PK" ON "MyTable" 
  AREA "Schema Area"
  UNIQUE
  PRIMARY
  INDEX-FIELD "Fld1" ASCENDING 
```
This should create a really simple table, with two fields, and a primary unique index.

Now, we'll create a new procedure, called src/test2.p :
```
CREATE MyTable.
ASSIGN MyTable.Fld1 = "ABC"
       MyTable.Fld2 = "DEF".
```
Now, add the following line after line 8 of the previous build.xml :
```xml
<mkdir dir="target/db" />
<PCTCreateDatabase dbName="db" destDir="target/db" schemaFile="db/db.df" dlcHome="${env.DLC}" />
```
and this one after line 10 :
```xml
<DBConnection dbName="db" dbDir="target/db" singleUser="true"/>
```
Now run Ant build from the shell prompt. You should get the following :
```
Buildfile: build.xml

build:
[PCTCreateDatabase] Copying DB /opt/dlc10/empty4 to target/db/db
[PCTCreateDatabase] Loading db/db.df in database
[PCTCompile] PCTCompile - Progress Code Compiler
[PCTCompile] 2 file(s) compiled

BUILD SUCCESSFUL
Total time: 7 seconds
```
Running ant build a second time will give you this :
```
Buildfile: build.xml

build:
[PCTCompile] PCTCompile - Progress Code Compiler
[PCTCompile] 0 file(s) compiled

BUILD SUCCESSFUL
Total time: 1 seconds
```

## Step 3 : propath

Imagine you'd like to work with PDFInclude : it would be a good idea to separate your own source code from PDFInclude source code, so that upgrading to a newer version would just be a drop of the new source files. So in project tree, you add a pdfinc-src directory, and include {pdfinc.i} in your programs. How to add this dir to your propath ? Quite simple, just add a propath directive in you PCTCompile task (line 9) :
```xml
<propath>
  <pathelement location="pdfinc-src"/>
</propath>
```
Compile as usual, using ant build, then execute build/test3.r : you should get
```
Message from pdfinc.i
Message from test3.p
```

## Step 4 : ADM2 and customizations

When working with ADM2, it's really a good idea to have your own copy in your project, so that you can upgrade your Progress version without upgrading your ADM2 version. Here is how I proceed : in my project tree, I create two subdirectories, called ade and ade-custom. The first one contains everything I import directly from Progress directory, and is only modified when I upgrade ADM2 version, the second one contains my own customizations.

Here is the target to compile the standard ADM2 :
```xml
  <target name="build-ade" description="Standard ADM2">
    <mkdir dir="build-ade" />
    <PCTCreateBase dbName="db" destDir="db" schemaFile="ade/temp-db.df" dlcHome="${env.DLC}" />
    <PCTCompile destDir="build-ade" dlcHome="${env.DLC}">
      <fileset dir="ade/src">
        <include name="adm2/**/*.p" />
        <include name="adm2/**/*.w" />
        <exclude name="adm2/template/**" />
      </fileset>
      <PCTConnection dbName="temp-db" dbDir="base/temp-db" singleUser="${singleUser}" />
      <propath>
        <pathelement location="ade" />
        <pathelement location="ade/src" />
      </propath>
    </PCTCompile>
    <copy toDir="ade">
      <fileset dir="ade/src">
        <include name="adm2/image/**" />
        <include name="adm2/template/**" />
      </fileset>
    </copy>
  </target>
```
And the target to compile your customized version of ADM2 :
```xml
  <target name="build-ade-custom" depends="build-ade" description="Customized ADM2">
    <mkdir dir="build-ade-custom" />
    <PCTCompile destDir="build-ade-custom" dlcHome="${env.DLC}">
      <fileset dir="ade/src">
        <include name="adm2/*.p" />
        <include name="adm2/*.w" />
      </fileset>
      <fileset dir="ade-custom/src">
        <include name="adm2/**/*.p" />
        <include name="adm2/**/*.w" />
        <exclude name="adm2/template/**" />
      </fileset>
      <PCTConnection dbName="temp-db" dbDir="base/temp-db" singleUser="${singleUser}" />
      <propath>
        <pathelement location="ade-custom" />
        <pathelement location="ade" />
        <pathelement location="ade/src" />
      </propath>
    </PCTCompile>
    <copy toDir="build-ade-custom">
      <fileset dir="ade-custom/src">
        <include name="adm2/image/**" />
        <include name="adm2/template/**" />
      </fileset>
    </copy>
  </target>
```

## Step 5 : let's proxygen...

We'll here explain how to use the Java proxygen. Using .Net and DLL proxygen should work identically.

In the provided example, we're using a Progress 10.0A XPXG file, but 9.1 PXG files are OK too.

Warning : 10.1 XPXG files don't work for now ; 10.1 doesn't accept relative paths anymore, which is really annoying...

Declaring a proxygen task is simple :
```xml
  <PCTProxygen workingDirectory="src" srcFile="src/MyApp.xpxg" dlcHome="${env.DLC}" />
```
Which gives the following result :
```
pxg:
[PCTProxygen] Batch ProxyGen, Version Progress 10.0A
[PCTProxygen] Generating Proxies...
[PCTProxygen] Proxy Generation Succeeded.
[PCTProxygen] For details see the log file  ..\build-pxg\MyProduct.log
```
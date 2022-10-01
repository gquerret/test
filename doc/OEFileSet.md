# OEFileSet

## Description

`<OEFileSet>` is a special form of a `<fileset>` which can be used to compile specific modules inside a source directory. It's a shortcut notation for the following syntax :
```
<fileset dir="src" includes="foo/**/*.p,foo/**/*.w,foo/**.cls" />
```
Which can be replaced by :
```
<OEFileSet baseDir="src" modules="foo" />
```

## Parameters

| **Attribute**| **Description**| **Type**| **Requirement**| **Default value**|
|:-------------|:---------------|:--------|:---------------|:-----------------|
|baseDir       |Dir attribute of fileset|File     |Required        |No default value  |
|modules       |Subdirectories in which to find .p, .w and .cls to be included|String   |Required        |No default value  |
|excludes      |Excludes pattern|String   |Optional        |No default value  |
|includeSubDirs|Also include procedures in sub-directories|Boolean  |Optional        |True              |
## Parameters as nested elements

Modules can be declared as nested elements. Modules have a single attribute name.

## Examples

```
<!-- Don't forget to declare types -->
<typedef resource="types.properties" />

<target name="copy">
  <PCTCompile destDir="build" dlcHome="${DLC}">
    <OEFileSet baseDir="src" modules="mfg,sal,acc" />
	<!-- Same fileset, but different syntax :
	<OEFileSet baseDir="src">
	  <Module name="mfg" />
	  <Module name="sal" />
	  <Module name="acc" />
	</OEFileSet> -->
  </PCTCompile>
</target>
```
Will compile every .p, .w and .cls in src/mfg, src/sal and src/acc, i.e. identical to :
```
  <fileset dir="src">
    <include name="mfg/**/*.p" />
    <include name="mfg/**/*.w" />
    <include name="mfg/**/*.cls" />
    <include name="sal/**/*.p" />
    <include name="sal/**/*.w" />
    <include name="sal/**/*.cls" />
    <include name="acc/**/*.p" />
    <include name="acc/**/*.w" />
    <include name="acc/**/*.cls" />
  </fileset>
```
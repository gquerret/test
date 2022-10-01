## Description
RCodeSelector is a selector in which files can be selected based on CRC or MD5 comparison in source and target directories. Files are removed of the fileset if and only if their CRC or MD5 are identical.

### Parameters

| **Attribute**| **Description**| **Default value**|
|:-------------|:---------------|:---------------:|
|dir †         |The base directory to look for the files to compare against. The precise location depends on a combination of this attribute and the `<mapper>` element, if any.|No default value  |
|lib †         |The procedure library to look for the files to compare against.|No default value  |
|mode          |Use MD5 or CRC to compare r-code|CRC               |

† Only one of those attributes is mandatory
‡ Mandatory attribute

## Parameters as nested elements

None

## Examples

```xml
<!-- Don't forget to include types definition -->
<typedef resource="types.properties" />

<target name="copy">
  <copy todir="destDir" includeEmptyDirs="false">
    <fileset dir="sourceDir1" includes="**/*.r">
      <RCodeSelector dir="sourceDir2" mode="md5" />
    </fileset>
  </copy>
</target>
</pre>
```
Will copy all .r files from sourceDir1 to destDir, excluding any r-code whose MD5 is identical in sourceDir1 and sourceDir2

## Notes

If you have IOException (usually with additional message `Resetting to invalid mark`), then you can increase the buffer size for RCodeInfo class by defining the Java property `rcodeinfo.buffer_size`. On the command line, this is done with:

```
set JAVA_OPTS=-Drcodeinfo.buffer_size=132000
ant target_name_here
```
Default size is 65536.

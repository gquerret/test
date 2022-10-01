# ProUnit task -- `<pct:prounit />`

## Description

Run a [ProUnit](http://prounit.sourceforge.net) tests sequence.

## Parameters

| **Attribute**| **Description**| **Type**| **Requirement**| **Default value**|
|:-------------|:---------------|:--------|:---------------|:-----------------|
|project       |ProUnit project file (xml)|File     |Required        |No default value  |
|result        |Results file name|File     |Optional        |No default value  |
|template      |Results format  |String   |Optional        |default           |
|compatibility |Use old procedure to run|Boolean  |Optional        |false             |

ProUnit inherits attributes from [PCTRun](PCTRun.md).

## Parameters as nested elements

## Examples
```
<ProUnit project="prounit.xml" result="resultProU.xml" dlcHome="${DLC}" template="default">
  <propath>
    <pathelement path="src" />
    <path location="foo\bar\prounit-directory\prounit_dlc11.pl" />
  </propath>
</ProUnit>
```
Run tests from the file 'prounit.xml' and throw results in 'resultProU.xml'. The default template generates XML files (non JUnit compliant).
The project file can be generated from the GUI (see Prounit documentation) or created by hand :
```
<?xml version="1.0" ?>
<ProUnitTestSuite>
  <plugins />
  <TestSet name="RSSW Tests" seq="1">
    <TestCase name="foo\bar\TestDirectory\Tests.p" seq="2" />
  </TestSet>
</ProUnitTestSuite>
```
Make sure to use the right version in your propath (prounit\_dlc11.pl, prounit\_dlc10.pl, prounit\_dlc9.pl).

## Results Templates
| **Name**| **Description**|
|:--------|:---------------|
|_builtin-CSV_|CSV             |
|_builtin-IndentedText_|Indented plain text|
|_builtin-JUnit_|JUnit XML       |
|A-ProUnitDefault\_XSL|Default XML with SLST|
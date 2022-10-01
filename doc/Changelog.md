# Changelog

## Version #222 (July 27th, 2022)
  * Support for tracing and trace-filter attributes in Profiler
  * Fix PLReader corner case issue when reading TOC

## Version #221 (September 8th, 2021)
  * Support for OpenEdge 12.4.
  * 12.4 has a critical issue with FILE-INFO (OCTA-39423), so use 12.4.1.

## Version #219 (July 30th, 2021)
  * DynamicRun now supports mainCallback attribute
  * Handle empty parameter attribute in PCTRun (issue #449)
  * Remove warning message when using PCTCompile in OE 11.6 and below (issue #451)
  * New JsonDocumentation task (will replace the other documentation task in next release)
  * Drop v10 code from the repository

## Version #218 (March 15th, 2020)
  * Fix issue #443 when using multi-thread compiler and warning 214
  * Add support for `requireReturnValue` in multi-thread compiler (fix by @clement-brodu)

## Version #217 (February 12th, 2021)
  * Add `property` attribute to `PCTVersion` task
  * Procedure `pct/dynrun.p` added as session super procedure in PCTDynamicRun

## Version #216 (December 22nd, 2020)
  * Dependency check when compiling classes (issue #62)
  * Upgraded the entire build chain to Java 11 while keeping runtime compatibility with Java 8 (so Java 7 is not supported anymore)
  * Compiler warnings can be forced in PCTCompile (issue #432)
  * ClientMode attribute in PCTRun
  * And other minor issues fixed since Feb. 2020

## Version #215 (February 7th, 2020)
  * New AssemblyCatalog task
  * New `encoding` attribute in ABLDuck (by @clement-brodu)
  * Multiple improvements in ABLDuck (by @clement-brodu)
  * New `requireReturnValues` attribute in PCTCompile

## Version #214 (November 28th, 2019)
  * OutputType attribute in PCTCompile

## Version #213 (September 19th, 2019)
  * Support for OpenEdge 12.1
  * Dropped support for OpenEdge 10
  * Fix for NPE in PCTBgCompile (issue #363)
  * Handle white spaces in Profiler:outputFile property (issue #374)
  * Buffer size when reading rcode can be set with Java property `rcodeinfo.buffer_size`
  * Add Option node to PCTBinaryDump and PCTBinaryLoad
  * Show message when xmlXref and stringXref are used at the same (this leads to a session crash)

## Version #212 (June 24th, 2019)
  * Support of early 11.x versions for compilation callback (#358) 
  * ABLUnit task: warning message if test directories not in propath
  * Fix NullPointerException in ABLDuck (#367)
  * IndexRebuild task
  * New RCodeMapper type, see [example](https://github.com/Riverside-Software/pct/wiki/PCTCompile#example-4)
  * OpenEdge 12 unit tests with OpenJDK 8 ant Ant 1.10

## Version #211 (March 20th, 2019)
  * **Fix issue in PCT 210 + OE12 where temp files were not deleted**
  * Callback support in PCTCompile (patch by @lievencardoen)
  * Listing page size and page width in PCTCompile (patch by @rubinhos)
  * Minor improvements in ABLDuck (patch by @spazzymoto)
  * paramFile attribute in PCTBinaryLoad (patch by @lievencardoen)

## Version #210 (March 1st, 2019)
  * PCT.jar now available on [Maven Central](https://mvnrepository.com/artifact/eu.rssw.pct/pct)
  * Fixed duplicate parameters problem in PCTRun (issue #308)
  * Fixed synchronization issue in multi-threaded compilation (issue #293)
  * Warning 4516 throwing STOP condition (issue #295)
  * XCode attribute regression in PCTCompile (issue #304)
  * RCodeSelector fix (issue #311)

## Version #209 (April 18th, 2018)
  * New [[ABLDuck]] task (Robert Edwards, MIP)
  * New [[PCTDynRun]] task
  * Various improvements in ClassDocumentation task
  * Compilation bug fix when using `xcode` option
  * Removed GenericCoverage task, in favor of the code coverage functionality in [SonarQube](https://github.com/Riverside-Software/sonar-openedge/wiki)
  * Added useRevvideo and useUnderline options in PCTCompile (issue #273)
  * destDir now optional in PCTCompile, defaults to source directory (issue #277)
  * Added XCodeSession attribute in PCTRun
  * PCT analyzed on http://sonar.riverside-software.fr with branch support :-)
  * XCode task speedup

## QA Build #208 (April 27th, 2017)
  * Improved error messages in case of compilation failure
  * Fixed issue #224: relative paths not handled in compilation error
  * Fixed issue #124: empty DF file shouldn't throw error in PCTLoadSchema
  * Support for 11.7
  * 11.7 strict mode compiler generates .warnings file
  * PCTASBroker and PCTWSBroker are back
  * Improve test cases duration (20% improvement on jenkins.rssw.eu)
  * Issue #183: warnings from -checkdbe reported in .warnings file
  * Issue #204: added quickRequest attribute in PCTRun / PCTBgRun
  * Issue #200: multi-threaded compilation could throw unexpected error
  * Issue #207: .xref file not deleted when compilation failed and `keepXref=false`
  * Issue #207: .warnings files not removed on rebuild
  * ENUM support and various fixes in ClassDocumentation
  * Upgrade to Ant 1.9.8
  * Upgrade to JDK 7

## QA Build #207 (Dec 21st, 2016)
  * **Dropped support for v8 and v9**
  * Force multi-threaded compilation when tag PCTCompileExt is used
  * Fixed issue #149 : NullPointerException in PCTCompile with multi-threading and multiple subfolders in destDir
  * Better code analysis on http://sonar.riverside-software.fr
  * Build system now using Jenkins 2 pipelines
  * Issue #177 : `pct:compile` style tag is broken since build 202
  * Issue #185 : NPE in case of invalid INI file
  * Translation Manager fixes
  * Issue #191 : fix for long XREF lines

## QA Build #206 (May 16th, 2016)
  * Removed verbose attribute from PCTRun; attribute is set automatically when -v (or -d) is provided on Ant command line
  * Issue #131 : missing error details when compiling xcoded files
  * Issue #127 : PCTCompile silently fails if preprocessDir directory does not exist
  * Issue #125 : new ignoreIncludes parameter in PCTCompile to ignore specific include files
  * Issue #72 : PCTCompile and PCTCompile now use the same codebase
  * PLReader can row read the table of content of memory-mapped PL
  * requireFullKeywords, requireFieldQualifiers, requireFullNames support in PCTCompile
  * GenericProfiler doesn't require guava and antlr4 in classpath anymore
  * Dropped Prolint task
  * Dropped PCTASBroker and PCTWSBroker tasks
  * Added displayFiles option in PCTCompile

## QA Build #202 (December 3rd, 2015)
  * `.warnings` file created in `.pct` subdirectory during compilation. Doesn't work with XREF-XML (bug reported to PSTS).
  * Issue #120 : fixed .inc generation problem with XML XREF
  * prolib.jar updated to extract files from command line
  * PLReader updated to read memory mapped PL files
  * Issue #122 : PCTCompileExt hangs when startup parameters are invalid

## QA Build #200 (September 21st, 2015)
  * [[RestGen]] task can be executed on UNIX (with a copy of $DLC/oeide directory)
  * [[ClassDocumentation]] update for 11.5 and above. **Build.xml and dependencies update required !**

## QA Build #198 (August 15th, 2015)
  * Added [[GenericCoverage]] task
  * Added flattenDbg attribute in [[PCTCompile]]
  * Fixed issue #76
  * Error handling in [[PCTProxygen]]
  * Changed version numbers in PCTVersion
  * Added ResourceCollection support to PCTProxygen (issue #97)
  * Fixed issue #31 (sourceDb attribute in PCTCreateBase)
  * Fixed issue #100 (override attributes in PCTConnection with refid)
  * Issue #101 : errorTolerance and srcDir in PCTLoadData

## QA Build #194 (March 13th, 2015)
  * Added pct:dlc\_home type
  * Added analyzerClass attribute to PCTLoadSchema
  * Added ~~errorPercentage~~ errorTolerance attribute to PCTLoadData
  * Added haltOnFailure attribute to ABLUnit
  * Merged PCTLoadData and PCTLoadDataCallback
  * No more 11.2 and 11.3 unit tests
  * Added 11.5 unit tests
  * Fixed GC bug #87 (on Google Code)
  * Fixed GC bug #79 (on Google Code)
  * Using matrix project for PCT unit tests : https://github.com/jakejustus/openedge-jenkins-plugin
  * PCTLibrary : destFile attribute is optional if sharedFile attribute is provided
  * Fixed GC bug #88 (on Google Code)

## QA Build #192 (November 15th, 2014)
  * **Download URL https://bitbucket.org/gquerret/pct/downloads/PCT-192.jar**
  * ~~Added PCTLoadDataCallback task~~
  * Added callback attribute to PCTLoadSchema
  * Added mainCallback attribute to PCTRun
  * Added DBAlias type to PCTRun

## QA Build #191 (November 1st, 2014)
  * **Download URL https://bitbucket.org/gquerret/pct/downloads/PCT-191.jar**
  * Added assemblies attribute to PCTCompileExt
  * GC bug #75 (on Google Code): problem with renameFile under 11.3 (PCTDumpIncremental). Fix provided by Robin Powell
  * Dump incremental updated for 11.4

## QA Build #190 (September 20th, 2014)
  * **Download URL https://bitbucket.org/gquerret/pct/downloads/PCT-190.jar**
  * Fixed problem with 11.4 and XML-XREF
  * Breaking change : debug listing files are generated in a different (and hopefully better) way. Blog post coming soon, please remind me to do it.

## QA Build #189 (August 23rd, 2014)
  * **Download URL https://bitbucket.org/gquerret/pct/downloads/PCT-189.jar**
  * Added OEUnit task
  * Handles debugListing and preprocess attributes with noParse=true
  * GC bug #63 (on Google Code) - Fix for class doc problem
  * No debug listing for files starting with underscore
  * Performance improvement when compiling large set of procedures/classes
  * GC bug #51 (on Google Code) : ClassDocumentation hanging on some classes
  * ClassDocumentation code and templates upgrade (by Consultingwerk)
  * GC bug #65 (on Google Code) : Fix for `_`TRAN collation in PCTCreateBase
  * GC bug #64 (on Google Code) : Incomplete listing files
  * GC bug #67 (on Google Code) : Statistics attribute in Profiler node
  * GC bug #68 (on Google Code) : assemblies attribute is skipped if file can't be found
  * Added listingSource attribute to PCTCompile

## QA Build #187 (June 4th, 2014)
  * **Download URL https://bitbucket.org/gquerret/pct/downloads/PCT-187.jar**
  * Fixed xmlXref attribute, build #186 was broken

## QA Build #186 (May 30th, 2014)
  * **Download URL https://bitbucket.org/gquerret/pct/downloads/PCT-186.jar**
  * Added auditing attribute to PCTCreateBase
  * Xcoded file content is not displayed anymore in case of compilation error
  * Added xmlXref attribute to PCTCompile (EDIT : bugs inside !)
  * Upgrading to Ant 1.9.4

## QA Build #185 (March 31st, 2014)
  * **Download URL https://bitbucket.org/gquerret/pct/downloads/PCT-185.jar** (Google closed download links)
  * Class documentation templates upgraded (Mike Fechner)
  * Test cases profiling
  * GC Bug #47 (on Google Code) : problem when importing XREF lines longer than 2000 chars
  * Added new task that shouldn't be named
  * Updated ProUnit task
  * QUIT statements can be trapped by PCTRun
  * RestGen task - First attempt
  * GC Bug #49 (on Google Code) : added v6frame attribute to PCTCompile / PCTCompileExt (legians)
  * Added relative and largeFiles attributes to PCTCreateBase (Carl Verbiest)
  * Separate rcode for 11.2 and 11.3
  * Running PCT with no PL in pct.jar was broken since build #183
  * Added stopOnError attribute to PCTCompile
  * Added OEFileSet nested parameter to PCTCompile
  * INI file attribute is skipped if file can't be found

## QA Build #184 (December 17th, 2013)
  * Fix for OE 11.3 64bits on Windows
  * Updated parser.jar : fixed isAbstract and isFinal on method nodes
  * Added newInstance attribute in PCTCreateBase (Paul Moberg)
  * Added debugPCT attribute to PCTLibrary (GC bug #45 (on Google Code))
  * Added method to read debug listing value in rcode
  * GC bug #42 (on Google Code) : `<propath>` not required anymore in ClassDocumentation
  * New code documentation tool from Consultingwerk

## QA Build #183 (September 25th, 2013)
  * Upgrading to Ant 1.9.1
  * Added multiTenant attribute to PCTCreateBase (by Havi)
  * Removed overwrite attribute in PCTCreateBase
  * Added collation option to PCTCreateBase (by Havi)
  * Added appendStringXref to PCTCompile (by Havi)
  * Added progPerc to PCTCompile (by Havi)
  * Added codepage options to PCTLibrary (by Havi)
  * New fields in XML schema output (by Havi)
  * Fixed some codepages issues in PCTRun (by Havi)
  * Added removeEmptyDFFile to PCTDumpIncremental (by Havi)
  * Some code reorg
  * Missing isFinal field in method documentation
  * GC bug #30 (on Google Code) : unable to reference pct:db\_connection in PCT tasks
  * GC bug #32 (on Google Code) : Procedure attribute in PCTRun is required

## Version 1.0 aka build #179 (June 9th, 2013)
  * Added stringXref attribute in PCTCompile/PCTCompileExt (by Havilog)
  * Added saveR attribute in PCTCompile/PCTCompileExt (by Havilog)
  * Added assemblies attribute in PCTRun
  * activeIndexes attribute is now an integer with following options (by Havilog)
    * 0 = all indexes active
    * 1 = all unique indexes inactive
    * 2 = all indexes inactive
  * Added ProLint task
  * Added encoding attribute to PCTDumpData
  * Added streamIO to PCTCompile/PCTCompileExt
  * Added OE 11 support
  * Added PCTDumpSequences task
  * Fixed bug #11 (on Google Code) (connection errors in PCTBgRun)
  * Added online attribute to PCTLoadSchema
  * PCTRun now accept DBConnection (replaces PCTConnection)
  * Rewrote TestNG tests in PCT, so that it's really easier to execute them under different OS and OpenEdge versions
  * Fixed bug #15 (on Google Code) : long file names in PCTLibrary
  * Upgrading to ANT 1.8.4
  * Correct behavior when working with different combinations of cpstream
  * Added preprocessDir attribute to PCTCompile/PCTCompileExt
  * Added ClassDocumentation task (JDK 6 required)
  * Added HTMLDocumentation task (OpenEdge 11.1 Windows required)
  * PCTConnection is now a DataType, thus can be declared in projet, and referenced in various tasks
  * Added sports2000 task
  * Using Java 5 syntax. This means that when working with old versions of Progress, you can't use the bundled JRE
  * Added verbose attribute in PCTRun
  * PCTLoadSchema now supports nested filesets
  * Added DlcHome task
  * Added relativePaths attribute in PCTCompile/PCTCompileExt
  * Added preprocessDir and debugListingDir in PCTCompile/PCTCompileExt
  * Added Profiler attribute to PCTRun
  * PCTLoadSchema, PCTCreateBase and PCTCompile now accept ResourceCollection instead of FileSets
  * Fixed bug #29 (on Google Code)
  * Added twoPass compilation attribute in PCTCompile
  * Added DBConnectionSet data type

## Version 0.18 (02/21/2011)
  * dbName is no longer required in PCTConnection. You have to use either dbName or paramFile. Allows full DB connection strings in paramFile
  * noError attribute in PCTAlias is handled correctly
  * Fixed incremental dump in 10.1C - Bug report by Jens Haubold
  * Fixed PLReader

## Version 0.17 (02/07/2011)
  * Several improvements on PLReader. Still one bug remaining when extracting adecomm.pl
  * Removed PLExtract task, in favor of PLFileSet type which can be nested in any FileSet capable task
    * Only in read tasks, PCTLibrary still needs to be used when creating libraries
  * Replaced CRCDifferent with RCodeSelector. Now able to use MD5 to compare r-code
  * Another bug when XREF when importing XREF on classes. Bug reported by Sascha Hofmann
  * Added environment variables to PCT tasks
  * If dlcHome attribute isn't set, try to use DLC property then DLC environment variable
  * PCTConnection was not allowing user name with no password. Enhancement by Sascha Hofmann
  * Upgrading to ANT 1.8
    * Edit : To 1.8.1
    * Edit : To 1.8.2
  * Changed the way $DLC/version is parsed. Thanks to Matt Baker for reporting bug and additional infos
  * Adding languages and textSegGrowth attributes to PCTCompile and PCTCompileExt tasks
  * Corrected warning message when compiling classes
  * antlib.xml for pct namespace was not included in JAR file
  * Updated documentation for pct namespace
  * Changed setPropath to addPropath in PCTRun, so that multiple propath definitions can be combined
  * Cleanup when tasks create a new subtask instance. Fixed a bug when using pct namespace
  * GC Bug #1 (on Google Code) : upgraded `pct/_dmpincr.p` to 10.2B
  * Added PCTVersion task
  * If pctX.pl is not available for your version of Progress, fall back to source code. Compilation licence required in this case.
  * Reads PCT-SRC property from the command line, to force source code instead of compiled version
  * GC Bug #2 (on Google Code) : more detailed error messages during connection (patch by Dan Dragut)

## Version 0.16 (10/01/2009)
  * Removed ping for statistics
  * Corrected bug when importing XREF on classes. Bug reported by Wytze Vlasman

## Version 0.15 (08/29/2009)
  * Added brokerLogFileAppend and serverLogFileAppend attributes to PCTASBroker and PCTWSBroker
  * Added keepXref attribute in PCTCompile
  * Corrected documentation for msgBufferSize attribute in PCTRun
  * Added jvmarg option to PCTProxygen
  * Added numThreads attribute in PCTCompileExt...
  * ... And rewrote PCTBgRun task
  * Server ping for statistics

## Version 0.14 (12/03/2008)
  * Added sharedFile attribute in PCTLibrary. Patch provided by Cameron David Wright
  * Fixed duplicate hierarchy when compiling .cls files. Bugfix provided by Peter KULLMANN
  * Added failOnError attribute in PCTRun. Patch provided by Peter KULLMANN
  * Upgrading to ANT 1.7.1
  * Added ProgressVersion task
  * Patch for PCTLibrary when filenames contains space. Patch provided by Nathanael SHERGOLD
  * Compilation and tests with OpenEdge 10.2 (replacing 10.1B)
  * Added resultProperty in PCTRun
  * Added OutputParameter in PCTRun

## Version 0.13 (11/18/2007)
  * Fixed keepFiles attribute in PCTProxygen. Bugfix provided by Michael Heist
  * Bug #1711731 (on Google Code) : fixed propath references
  * Added error message when dlcHome attribute is not defined. Prevents hard-to-understand further error messages
  * Added PROPATH and DB Connection support in PCTASBroker task. Enhancement provided by Evan Todd
  * Added unfreeze option in PCTLoadSchema task. Enhancement provided by Evan Todd
  * Added Table attribute in PCTLoadData task. Enhancement provided by Evan Todd
  * Added debugListing attribute in PCTCompile task
  * Added support for 64 bits Progress
  * Fixed problem with PCTBinaryDump under UNIX systems
  * Added PCTCompileExt task

## Version 0.12a (01/30/2007)
  * Fixed PCTDumpSchema task (invalid procedure call)

## Version 0.12 (01/27/2007)
  * Added testcase for RCodeInfo
  * Upgrading to JUnit 4.1
  * Bug #1507272 (on Google Code) : added PCTWSBroker task
  * Bug #1566571 (on Google Code) : corrected failed compilation warning when fileset not in PROPATH
  * Updated developer's documentation
  * Limited support for Progress 8
  * Upgrading to ANT 1.7
  * Added Parameter nested attribute to PCTRun
  * Changed schema holders support in PCTCreateBase
  * Updated PCTDumpIncremental support with v9
  * Added CRCDifferent custom selector

## Version 0.11 (09/12/2006)
  * Corrected bug when temp directory contains '~' character (e.g. on Windows when using C:\DOCUME~1\login\LOCALS~1\Temp). Added testcase for this bug. Bugfix provided by Peter KULLMANN
  * Bugfix : temp files deletion in PCTRun task (and subtasks) when an unknown procedure was defined
  * Fixed compatibility with upcoming 1.7 ANT release

## Version 0.10 (06/10/2006)
  * Added PCTBinaryDump task
  * Added listing and preprocess attributes in PCTCompile task
  * Added schema holder support in PCTCreateBase
  * Added wordRules option in PCTCreateBase
  * Added PCTASBroker task to create/remove/update appservers definition
  * Bug #1455512 (on Google Code) : corrected bug on include/exclude patterns in PCTBinaryDump
  * No need to copy tty/ and gui/ subdirs in $DLC. Everything is included in PCT.jar (both v9 and v10). The Progress version used is auto-detected.
  * Corrected crash when using a DB connection where directory name contains spaces

## Version 0.9 (07/10/2005)
  * Upgrading to ANT 1.6.5
  * Manifest in PCT.jar
  * Added debugReady parameter in PCTRun task
  * Useless i18n :-)
  * Bug #1245992 (on Google Code) : PCTCreateBase, schema files and absolute paths
  * Added tempDir and baseDir attributes to PCTRun task
  * Feature request #1229640 : PCTLoadData task (really really simple version at the moment)
  * Bug #1276486 (on Google Code) : patch from Flavio Cordova (bug not closed for now, waiting for further testing)
  * Feature request #1276506 : now possible to add custom parameters in PCTRun
  * Added a ProUnit task
  * JUnit reports in documentation
  * Bug #1311746 (on Google Code) : mixed case extension are not handled correctly.
  * Always forking Java task : the previous behaviour was to fork only when working directory was specified.

## Version 0.8 (05/13/2005)
  * PCT can be compiled with JDK 1.5 (just added source attribute in javac task)
  * Bug #1114731 (on Google Code) : new way of handling JAR dependencies. Warning : API changed, see PCT.java and PCTProxygen.java for details. Corrected twice (for OE 10.0B02)
  * Bug #1117740 (on Google Code) : DLC environment not defined. Added DLC environment variable in every Exec or Java task.
  * Added Eclipse stuff in CVS...
  * Added quickstart HTML page
  * Multiple files can be loaded in a single PCTCreateBase statement

## Version 0.7 (01/17/2005)
  * Added screenshots to website
  * Bug #1081206 (on Google Code) : added messages.jar to classpath in proxygen task (for 9.1d and upper)
  * Bug #1081209 (on Google Code) : in proxygen task, java process is forked
  * Bug #1102998 (on Google Code) : corrected bug in PCTSchemaDoc with codepage and collation
  * Added runList attribute in PCTCompile task, which checks for RUN statements
  * Bug #1103002 (on Google Code) : added case-sensitive attribute in ttTimeStamps which records included files

## Version 0.6 (11/04/2004)
  * Bug #995235 (on Google Code) : compress command line is only run once
  * Added codepage attribute to PCTCreateBase to create database with a specific codepage
  * Bug #1020999 (on Google Code) : cheks the .pl created is not in the file list
  * Bug #995235 (on Google Code) : added basedir, includes, excludes, includesfile, excludesfile, defaultexcludes attribute to the PCTLibrary task
  * Behavior change in the PCTLibrary task : task fails when no filesets defined (either with basedir or nested fileset). Previous behavior was to create an empty library.
  * Added numsep and numdec attributes to PCTRun task
  * Bug #1058733 (on Google Code) : multiple assignments for propath in PCTRun

## Version 0.5 (08/25/2004)
  * Bug #972486 (on Google Code) : changed the way temp files are deleted
  * Bug #992280 (on Google Code) : added paramFile attribute to PCTConnection

## Version 0.5 pre2 (06/10/2004)
  * Added PCTXCode task (Dick Knol)
  * Added noCompile and xcode attributes in PCTCompile
  * Separate versions for Progress v9 and v10
  * Removed Jalopy for Eclipse formatting
  * Added Propath to PCTCreateBase
  * Added PCTDumpData task (Dick Knol)
  * Corrected PCTIncrementalDump bug (Dick Knol)
  * Added parameterFile attribute in PCTRun
  * PCTSchemaDoc now creates XML file. It has to be tied with a style task

## Version 0.5 pre1 (05/13/2004)
  * PCTCRC task (Dick Knol)
  * Documentation update
  * New compilation procedure : now checks CRC, so database updates force recompilation
  * Added iniFile and ttBufferSize attributes in PCTRun
  * Changed the way temp files are deleted. Should work better, but still not perfect

## Version 0.4 (01/18/2004)
  * Added hasNamedAlias method in PCTConnection (P. BAIRD)
  * Added PCTWSComp task - Not tested, so don't expect it to run correctly. Help needed for this task, as I don't know how WebSpeed works
  * Added PCTBinaryLoad task
  * Updated PCTCreateBase :
    * Removed noSchema attribute (use directly structFile)
    * Added schemaFile attribute (loads a .df into database after its creation)
    * Corrected bug when destDir == null
    * Added unit tests
  * Added debugPCT attribute in PCTRun (protected, so it can accessed from children)
  * Changed the way files are added in PCTCompile and PCTWSComp (should no more block on large filesets)
  * Added PCTDumpIncremental task. Not really tested. (P. BAIRD)
  * Documentation cleanup
  * Added more JUnit tests

## Version 0.3b (11/15/2003)
  * Added unit tests (still in development)
  * Added website task
  * Updated download webpage
  * Updated jar task (files were added twice)
  * Added forceCompile attribute to PCTCompile
  * Added com.phenix.pct.PLReader task and documentation

## Version 0.3a
  * Changed the way files are handled in the PCTCompile

## Version 0.3 (09/29/2003)
  * Documentation updated
  * Added checkstyle task in build.xml (internal)
  * Major rewrite (conforming to ANT standards)
  * Added pctProxygen task
  * Added pctRun task
  * Resource properties file added in JAR
  * Progress source files moved to pct subdir

## Version 0.2 (07/15/2003)
  * Documentation included in tarball & minor changes
  * PCTCreateBase : added destDir attribute
  * PCTCompile : logs how many files were compiled or not
  * PCTCompile : automatically creates subdirectories during the build process
  * PCTCompile : uses XREF to compile only modified files
  * PCTDumpSchema, PCTLoadSchema, PCTSchemaDoc : changed the way it handles PCTConnection
  * PCTLibrary : added the noCompress attribute (false by default)

## Version 0.1 (06/05/2003)
  * First alpha release
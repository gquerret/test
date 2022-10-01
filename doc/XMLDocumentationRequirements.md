*Extract of [Mike Fechner](https://github.com/mikefechner) presentation*

### Class Browser documentation
* View in Progress Developer Studio for OpenEdge
* OO programmers best friend
* "Initialize OpenEdge Tooling" provides list of classes and members (methods / properties / events)
* Comments or further documentation only provided for ABL build-in objects and .NET classes

### Class Browser documentation
* This is **undocumented**... and **may change at anytime** (but it hasn‘t changed in the last 8 OpenEdge releases!)
* You can provide an XML file in a specific format
* XML file must reside in the project root folder that contains classes
* XML file must be named after the physical root folder this project resides in – NOT the project name, e.g. `ABL.xml` when source is in `C:\Work\SmartComponents4NET\Trunk\ABL`

### Class Browser documentation
* <documentation>.xml can be generated from the same class documentation output as the HTML documentation
* Makes first time opening of the Class Browser a bit slower
* Limitation: XML file does not support providing separate documentation entries for overloaded methods (polymorphic methods)

[[images/PDS-ClassDoc.png]]


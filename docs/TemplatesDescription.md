# Templates description

The following templates are used to define the HTML output :
  * Index.template
  * Document.template
  * DocumentDetails.template
  * DocumentDetailsParameter.template
  * DocumentList.template
  * DocumentListItem.template
  * DocumentOverview.template

### Index.template
This template defines the startpage (index.html) in the HTML documentation. You can add your company logo or define your own corporate layout.

### Document.template
This template defines the output of all methods, properties, interfaces and constructors of a class. The html shows an overview and a detail view of all class members. You can define your own layout and/or add javascript functionality.

### DocumentDetails.template
This template defines the output for the detail view of a class member. You may apply any style and layout to the document as you want.

### DocumentDetailsParameter.template
This template defines the layout for the parameter and return value texts. The output result will be arranged by the definitions in the DocumentDetails.template.

### DocumentList.template
This template defines the class overview on the left side. Here you may apply a different layout or you can implement javascript functionality to show the class overview in a modern tree style.

### DocumentListItem.template
This template defines the layout of an entry in the class overview which is used in the DocumentList.template to build the class overview. Here you can manipulate the output from the class link.

### DocumentOverview.template
This template defines the output for the overview showing all members of the class. You may apply any style and layout to the document as you want.

The following place holder can be used in that define templates:

| **Name** | **Replaced by** | **Supported Templates** |
|:---------|:----------------|:------------------------|
| @PAGETITLE@ | The title from the html document. You can set the DocumentationTitle property | DocumentList.template Document.template Index.template |
| @CONTENT@ | All generated DocumentListItems (Navigation-Links) | DocumentList.template   |
| @NAME@   | Method-, event- or propertyname | DocumentOverview.template DocumentDetails.template |
| @SIGNATURE@ | The full signature example: METHOD PRIVATE MyMethod (myParam AS CHARACTER) | DocumentOverview.template DocumentDetails.template |
| @SHORTSIGNATURE@ | The short signature example: MyMethod (CHARACTER) | DocumentOverview.template DocumentDetails.template |
| @PURPOSE@ | The purpose comment | DocumentOverview.template DocumentDetails.template |
| @COMMENT@ | The formatted comment block | DocumentOverview.template DocumentDetails.template |
| @MODIFIER@ | The modifier public, private or protected | DocumentOverview.template DocumentDetails.template |
| @SHORTMODIFIER@ | The short modifier : `+` public `-` private `#` protected | DocumentOverview.template DocumentDetails.template |
| @ISSTATIC@ | Return a charcter value true or false | DocumentOverview.template DocumentDetails.template |
| @RETURNTYPE@ | The return type of a method | DocumentOverview.tempate DocumentDetails.template |
| @ISABSTRACT@ | Return a character value true or false | DocumentOverview.tempate DocumentDetails.template |
| @DELEGATENAME@ | The delegate name of an event | DocumentOverview.tempate DocumentDetails.template |
| @SETMODIFIER@ | The set modifier of an event | DocumentOverview.tempate DocumentDetails.template |
| @GETMODIFIER@ | The get modifier of an event | DocumentOverview.tempate DocumentDetails.template |
| @GUID@   | A GUID that will be used for the top link navigation | DocumentOverview.tempate DocumentDetails.template |
| @PARAMETERNAME@ | The paramtername | DocumentDetails Paramter.template |
| @PARAMETERPOSITION@ | The position of parameter | DocumentDetailsParameter.template |
| @PARAMETERDATATYPE@ | The datatype from the parameter | DocumentDetailsParamter.template |
| @PARAMTERMODE@ | The mode from the parameter. Input, output or input-ouput | DocumentDetailsParamter.template |
| @PARAMTERFULLDATATYPE@ | Return a html-link when the fulldatatype is a class (no support for .Net classes), otherwise a character string. | DocumentDetailsParamter.template |
| @PARAMETERCOMMENT@ | The comment from the paramter | DocumentDetailsParamter.template |
| @CLASSNAME@ | The filenames from the xml source-directory | DocumentListItem.template |
| @HREF@   | The html link to the document | DocumentListItem.template |
| @PACKAGENAME@ | The the packagename | Document.template       |
| @CLASSNAME@ | The classname   | Document.template       |
| @INHERITS@ | The inherited class | Document.template       |
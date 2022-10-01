# Standard comment block

```
/*------------------------------------------------------------------------------
	Purpose: 
	Notes:   
	@param parameter1 Description
	@return 
 ------------------------------------------------------------------------------*/
```

The comment parser checks every line if it starts with `/*-` or `---` and removes it. Therefore you should never use those characters at the beginning of a line, you want to output.

When you provide a documentation from a parameter in the comment block, you should use the following format:
```
@param parameter1 Description
```

All parameter comments have a special HTML-Output, when you don't use `@param`, the comment parser cannot recognize the parameter descriptions.
Make sure to separate the parts of the parameter description by whitespaces cause that's the way to separate the strings for the documentation.

If you wish to provide documentation for return value of a method (not VOID) then you can use the `@return` describer to provide a return description.

There is no parameter name for the return value so you just add a description to the marker separated with a whitespace

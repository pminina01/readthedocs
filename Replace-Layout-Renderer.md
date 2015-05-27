Replaces a string in the output of another layout with another string. 

Supported in .NET, Silverlight, Compact Framework and Mono.

##Configuration Syntax
```
${replace:searchFor=String:wholeWords=Boolean:replaceWith=String
         :ignoreCase=Boolean:regex=Boolean:inner=Layout}
```

##Parameters
###Search/Replace Options
* _searchFor_ - Text to search for.
* _wholeWords_ - Indicates whether to search for whole words. Boolean
* _replaceWith_ - Replacement string.
* _ignoreCase_ - Indicates whether to ignore case when searching. Boolean
* _regex_ - Indicates whether regular expressions should be used when searching. Boolean

###Transformation Options
* _inner_ - Wrapped layout. Layout

##example
Replace newlines with `-`

```xml
<variable name="replacedname" 
  value="${replace:searchFor=\\n+:replaceWith=-:regex=true:inner=${message}} />
```
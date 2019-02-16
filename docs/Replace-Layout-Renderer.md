Replaces a string in the output of another layout with another string. 

Supported in .NET, Silverlight, Compact Framework and Mono.

## Configuration Syntax
```
${replace:searchFor=String:wholeWords=Boolean:replaceWith=String
         :ignoreCase=Boolean:regex=Boolean:inner=Layout}
```

## Parameters
### Search/Replace Options
* **searchFor** - Text to search for.
* **wholeWords** - Indicates whether to search for whole words. Boolean
* **replaceWith** - Replacement string.
* **ignoreCase** - Indicates whether to ignore case when searching. Boolean
* **regex** - Indicates whether regular expressions should be used when searching. Boolean

### Transformation Options
* **inner** - Wrapped layout. Layout

## Example
Replace newlines with `-`

```xml
<variable name="replacedname" 
  value="${replace:searchFor=\\n+:replaceWith=-:regex=true:inner=${message}}" />
```
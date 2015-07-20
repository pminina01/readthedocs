Replaces a new lines in the output of another layout with a string.

Added in NLog 4.1

Supported in .NET, Silverlight, Compact Framework and Mono.

# Configuration Syntax
`${replace-newlines:replacement=String}`

## Parameters
_replacement_ - Text to replace newlines with. Default is `" "` (space)

##Examples

Examples are using the MDC:

```c#
MappedDiagnosticsContext.Set("foo", "bar" + System.Environment.NewLine + "123");
```

###To space
```
${replace-newlines:${mdc:foo}}
```
Will result in "bar 123"

###To other char
```
${replace-newlines:replacement=|:${mdc:foo}}
```
Will result in "bar|123"




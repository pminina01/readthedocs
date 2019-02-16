A string literal. 

Supported in .NET, Silverlight, Compact Framework and Mono.

## Configuration Syntax
```
${literal:text=String}
```

## Parameters
### Rendering Options
* **text** - Literal text.
 
## Remarks
This is used to escape `'${' sequence as ;${literal:text=${}'`.

## Examples
### Basic
Configuration:
```
${literal:text=Some Text with ${ in it}
```
Code:
```
logger.Debug("Test Message")
```
Result:
```
Some Text with ${ in it
```
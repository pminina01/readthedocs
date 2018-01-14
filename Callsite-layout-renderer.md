The call site (class name, method name and source information). 

Supported in .NET, Silverlight and Mono.

## Configuration Syntax
```
${callsite:className=Boolean:fileName=Boolean:includeSourcePath=Boolean:methodName=Boolean}
```

## Parameters
### Rendering Options
* **className** - Indicates whether to render the class name.Boolean Default: `True`
* **includeNamespace** - Include namespace in class name? Boolean Default: `True`
  > Introduced with NLog v4.4
* **fileName** - Indicates whether to render the source file name and line number.Boolean Default: `False`
* **includeSourcePath** - Indicates whether to include source file path.Boolean Default: `True`
* **methodName** - Indicates whether to render the method name.Boolean Default: `True`
* **cleanNamesOfAnonymousDelegates** - Indicates whether the method name will be cleaned up if it is detected as an anonymous delegate. Boolean Default: `False`
  > Introduced with NLog v4.3.9
* **cleanNamesOfAsyncContinuations** - Indicates whether the method and class names will be cleaned up if it is detected as an async continuation. Boolean Default: `False`
  > Introduced with NLog v4.5
* **skipFrames** - The number of frames to skip. Integer Default: `0`

## Notes
please note that the method name won't work well with async methods before NLog 4.3 - it will always show `MoveNext`. 
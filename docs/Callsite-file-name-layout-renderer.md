The call site source file name. For full callsite use [CallSiteLayoutRenderer](Callsite-Layout-Renderer)

Introduced in NLog v4.5

Supported in .NET and Mono.

## Configuration Syntax
```
${callsite-filename:includeSourcePath=Boolean:skipFrames=Integer}
```

## Parameters
### Rendering Options
* **includeSourcePath** - Shows the full path of the source file. Boolean Default: True
* **skipFrames** - The number of frames to skip. Integer Default: 0

## Notes
Please also note that this infers heavy performance hit when doing lots of logging, as it has to capture full StackTrace for every log message.
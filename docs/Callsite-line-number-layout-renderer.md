The call site source line number. For full callsite use [CallSiteLayoutRenderer](Callsite-Layout-Renderer)

Introduced in NLog v4.1

Supported in .NET and Mono.

## Configuration Syntax
```
${callsite-linenumber:skipFrames=Integer}
```

## Parameters
### Rendering Options
* **skipFrames** - The number of frames to skip. Integer Default: 0

## Notes
Please also note that this infers heavy performance hit when doing lots of logging, as it has to capture full StackTrace for every log message.
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
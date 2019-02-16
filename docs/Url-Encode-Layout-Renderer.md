Encodes the result of another layout output for use with URLs. 

Supported in .NET, Silverlight, Compact Framework and Mono.

## Configuration Syntax
```
${url-encode:spaceAsPlus=Boolean:inner=Layout}
```

## Parameters
### Transformation Options
* **spaceAsPlus** - Indicates whether spaces should be translated to '+' or '%20'. Boolean
* **inner** - Wrapped layout. Layout
* **escapeDataRfc3986** - NLog will by default encode as UTF8 and escape special characters according to Rfc2396. To escape data according to standard Rc3986, set this option to 'true' (Available from NLog 4.4)
* **escapeDataNLogLegacy** - NLog will by default encode as UTF8 and escape special characters according to Rfc2396. To escape data according to the old non-standard NLog style, set this option to 'true' (Available from NLog 4.4)
Render the application domain name.

From NLog 4.0+, in NLog.Extended

##Configuration Syntax
```
${appdomain:format=Format}
```

##Parameters
###Rendering Options
**format - The formating.  Default to `Long`.
possible options:
* Long: default. The id as four number digit, colon, friendlyname. E.g. 0003:NLog.UnitTests
* Short. Only the id as two number digit, like "03".
* or custom like {0} -  {1}. The first parameter is the"AppDomain.Id", the second is the "AppDomain.FriendlyName". Note: use escaping of the brackets. See examples.


##Example
Examples in the .config

```xml
${appdomain} //e.g. 0003:NLog.UnitTests
${appdomain:format=short} //e.g. 03
${appdomain:format=long} //e.g. 0003:NLog.UnitTests
${appdomain:format={1\} - {0\}} //e.g. NLog.UnitTests - 3


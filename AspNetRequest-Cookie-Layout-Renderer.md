Introduced in NLog.Web 4.3

ASP.NET Request Cookie key/value pairs. 

Supported in ASP.NET, ASP.NET Core and Mono

## Configuration Syntax
```
${aspnet-request-cookie:cookieNames=String[]:outputFormat=Enum
    :itemSeparator=String:valueSeparator=String
    :singleAsArray=Boolean:valuesOnly=Boolean}
```

## Parameters
### Rendering Options
* **cookieNames** - Cookie key name(s). A list of keys can be passed as comma separated values, e.g.: `Key1,Key2`

### Formatting options
* **outputFormat** - Renders as flat string or JSON array. Possible values: `Flat`, `Json`. Default: `Flat`.
* **itemSeparator** Separator between items. Default: `,`. Only applies when OutputFormat is `Flat`. Introduced in NLog.Web.AspNetCore 4.4  / NLog.Web 4.5 
* **valueSeparator** Separator between value and key. Default: `=`. Only applies when OutputFormat is `Flat`. Introduced in NLog.Web.AspNetCore 4.4  / NLog.Web 4.5 
* **singleAsArray** Single item in array? If false, then a single item will be a single object. Only used when OutputFormat is `Json`. Default: `true`. Introduced in NLog.Web.AspNetCore 4.4  / NLog.Web 4.5 
* **ValuesOnly** Only render the values of the key/value pairs. Default: `false`. Introduced in NLog.Web / NLog.Web.AspNetCore 4.6


## Remarks
Use this layout renderer to log the value of the specified cookie(s) stored in the ASP.NET Request Cookies collection.

## Examples

In C# code:
```c#
Request.Cookies["username"] = "johnDoe";
Request.Cookies["id"] = "d4b20a34-6231-4201-83a6-c72599e41164";
```

### Log single cookie in default Flat output format
```
${aspnet-request-cookie:CookieNames=username}
```
Will print:
```
"username=JohnDoe"
```

### Log multiple cookies in default Flat output format
```
${aspnet-request-cookie:CookieNames=username,id}
```
Will print:
```
"username=JohnDoe,id=d4b20a34-6231-4201-83a6-c72599e41164"
```

### Log single cookie in JSON output format
```
${aspnet-request-cookie:CookieNames=username:OutputFormat=JSON}
```
Will print:
```json
[{"username":"JohnDoe"}]
```

### Log multiple cookies in JSON output format
```
${aspnet-request-cookie:CookieNames=username,id:OutputFormat=JSON}
```
Will print:
```json
[{"username":"JohnDoe","id":"d4b20a34-6231-4201-83a6-c72599e41164"}]
```

### Log single cookie in JSON output format with SingleAsArray=false
```
${aspnet-request-cookie:CookieNames=username:OutputFormat=JSON:SingleAsArray=false}
```
Will print:
```json
{"username":"JohnDoe"}
```

### Log single cookie in Flat output format as value only
```
${aspnet-request-cookie:CookieNames=username:ValuesOnly=true}
```
Will print:
```
"JohnDoe"
```

### Log single cookie in JSON output format as value only
```
${aspnet-request-cookie:CookieNames=username:OutputFormat=JSON:ValuesOnly=true}
```
Will print:
```json
["JohnDoe"]
```

### Log multiple cookies in JSON output format as value only
```
${aspnet-request-cookie:CookieNames=username:OutputFormat=JSON:ValuesOnly=true}
```
Will print:
```json
["JohnDoe","d4b20a34-6231-4201-83a6-c72599e41164"]
```

Introduced in NLog.Web 4.3

ASP.NET Request Query String key/value pairs. 

Supported in .NET, .NET Core and Mono

## Configuration Syntax
```
${aspnet-request-querystring:queryStringKeys=String[]:outputFormat:Enum
    :itemSeparator=String:valueSeparator=String
    :singleAsArray=Boolean:valuesOnly=Boolean}
```

## Parameters
### Rendering Options
* **queryStringKeys** - Query String key(s). A list of keys can be passed as comma separated values, e.g.: `Key1,Key2`. Became optional in NLog.Web 4.3.1, where no value will log all key/value pairs.

### Formatting options
* **outputFormat** - Renders as flat string or JSON array. Possible values: `Flat`, `Json`. Default: `Flat`.
* **itemSeparator** Separator between items. Default: `,`. Only applies when OutputFormat is `Flat`. Introduced in NLog.Web.AspNetCore 4.4  / NLog.Web 4.5 
* **valueSeparator** Separator between value and key. Default: `=`. Only applies when OutputFormat is `Flat`. Introduced in NLog.Web.AspNetCore 4.4  / NLog.Web 4.5 
* **singleAsArray** Single item in array? If false, then a single item will be a single object. Only used when OutputFormat is `Json`. Default: `true`. Introduced in NLog.Web.AspNetCore 4.4  / NLog.Web 4.5 
* **ValuesOnly** Only render the values of the key/value pairs. Default: `false`. Introduced in NLog.Web / NLog.Web.AspNetCore 4.6


## Remarks
Use this layout renderer to insert the value of the specified query string parameters stored in the ASP.NET Query String collection.

## Examples

In C# code:
```c#
Response.Redirect("myPage.aspx?key1=value1&id=d4b20a34-6231-4201-83a6-c72599e41164");
```

### Log single query string key/value pair in default Flat output format
```
${aspnet-request-querystring:QueryStringKeys=key1}
```
Will print:
```
"key1=value1"
```

### Log multiple query string key/value pairs in default Flat output format
```
${aspnet-request-querystring:QueryStringKeys=key1,id}
```
Will print:
```
"key1=value1,id=d4b20a34-6231-4201-83a6-c72599e41164"
```

### Log single query string key/value pair in JSON output format
```
${aspnet-request-querystring:QueryStringKeys=key1:OutputFormat=JSON}
```
Will print:
```json
[{"key1":"value1"}]
```

### Log multiple query string key/value pairs in JSON output format
```
${aspnet-request-querystring:QueryStringKeys=key1,id:OutputFormat=JSON}
```
Will print:
```json
[{"key1":"value1","id":"d4b20a34-6231-4201-83a6-c72599e41164"}]
```

### Log single query string key/value pair in JSON output format with SingleAsArray=false
```
${aspnet-request-querystring:QueryStringKeys=key1:OutputFormat=JSON:SingleAsArray=false}
```
Will print:
```json
{"key1":"value1"}
```

### Log single query string key/value pair in Flat output format as value only
```
${aspnet-request-querystring:QueryStringKeys=key1:ValuesOnly=true}
```
Will print:
```
"value1"
```

### Log single query string key/value pair in JSON output format as value only
```
${aspnet-request-querystring:QueryStringKeys=key1:OutputFormat=JSON:ValuesOnly=true}
```
Will print:
```json
["value1"]
```

### Log multiple query string key/value pairs in JSON output format as value only
```
${aspnet-request-querystring:QueryStringKeys=key1,id:OutputFormat=JSON:ValuesOnly=true}
```
Will print:
```json
["value1","d4b20a34-6231-4201-83a6-c72599e41164"]
```

Introduced in NLog.Web 4.7

ASP.NET Request Form key/value pairs. 

Supported in ASP.NET, ASP.NET Core and Mono

## Configuration Syntax
```
${aspnet-request-form:include=String[]:exclude=String[]:outputFormat=Enum
    :itemSeparator=Layout:valueSeparator=Layout
    :singleAsArray=Boolean:valuesOnly=Boolean}
```

## Parameters
### Rendering Options
* **include** - Form key name(s) to include in the output. A list of keys can be passed as comma separated values, e.g.: `Key1,Key2`. Optional, no value will log all key/value pairs not specifically excluded. If the same key is in both include and exclude, exclude takes precedence over include.
* **exclude** - Form key name(s) to exclude from the output. A list of keys can be passed as comma separated values, e.g.: `Key1,Key2`. Optional, no value will not exclude any. If the same key is in both include and exclude, exclude takes precedence over include.

### Formatting options
* **outputFormat** - Renders as flat string or JSON array. Possible values: `Flat`, `Json`. Default: `Flat`.
* **itemSeparator** Separator between items. Default: `,`. Only applies when OutputFormat is `Flat`.
* **valueSeparator** Separator between value and key. Default: `=`. Only applies when OutputFormat is `Flat`.
* **singleAsArray** Single item in array? If false, then a single item will be a single object. Only used when OutputFormat is `Json`. Default: `true`. 
* **ValuesOnly** Only render the values of the key/value pairs. Default: `false`.


## Remarks
Use this layout renderer to log the ASP.NET Request Form collection.

## Examples

In C# code:
```c#
httpContext.Request.Form = new FormCollection(new Dictionary<string, StringValues>{
    { "id","1" },
    { "name","Test Person" },
    { "token","86abe8fe-2237-4f87-81af-0a4e522b4140" }
}); 
```

### Log all Form data from the Request in default Flat output format
```
${aspnet-request-form}
```
Will print:
```
"id=1,name=Test Person,token=86abe8fe-2237-4f87-81af-0a4e522b4140"
```

### Log all Form data from the Request in JSON output format
```
${aspnet-request-form:OutputFormat=JSON}
```
Will print:
```
[{"id":"1"},{"name":"Test Person"},{"token":"86abe8fe-2237-4f87-81af-0a4e522b4140"}]
```

### Log only the specified Form keys from the Request in default Flat output format
```
${aspnet-request-form:Include=id,name}
```
Will print:
```
"id=1,name=Test Person"
```

### Log all Form data from the Request except for the specified keys in default Flat output format
```
${aspnet-request-form:Exclude=token}
```
Will print:
```
"id=1,name=Test Person"
```

### Log all Form data from the Request in Flat output format with each item separated by a new line
```
${aspnet-request-form:ItemSeparator=${newline}}
```
Will print:
```
"id=1\r\nname=Test Person\r\ntoken=86abe8fe-2237-4f87-81af-0a4e522b4140"
```
Exception information provided through a call to one of the Logger.*Exception() methods. 

Supported in .NET, Silverlight, Compact Framework and Mono.

## Configuration Syntax
```
${exception:innerFormat=String:maxInnerExceptionLevel=Integer:innerExceptionSeparator=String
           :separator=String:format=String:exceptionDataSeparator=string}
```

## Parameters
### Rendering Options
* **format** - Format of the output. Must be a comma-separated list of exception properties: `Message`, `Type`, `ShortType`, `ToString`, `Method`, `StackTrace`, `Data` & `@`. This parameter value is case-insensitive. Default: `message`
  * `@` means serialize all Exception-properties into Json-format. Introduced in NLog 4.5

* **innerFormat** - Format of the output of inner exceptions. Must be a comma-separated list of exception properties: `Message`, `Type`, `ShortType`, `ToString`, `Method`, `StackTrace`, `Data` & `@`. This parameter value is case-insensitive. 

* **maxInnerExceptionLevel** - Maximum number of inner exceptions to include in the output. By default inner exceptions are not enabled for compatibility with NLog 1.0.Integer. Default: 0

* **separator** - Separator used to concatenate parts specified in the Format. Default: single space
* **innerExceptionSeparator** - Separator between inner exceptions. Default: new line
* **exceptionDataSeparator** -  Separator used to concatenate the exception data parts. Default: `;`. Introduced in NLog 4.3.9

## Examples

### Log only message
Only message of the first exception

```
${exception}
```
or
```
${exception:format=message}
```


### Log full (but without Data)
`ToString` is also printing the innerExceptions

```
${exception:format=toString}
```

### Log full
Also print exception data, e.g.

```c#
var ex = new Exception();
ex.Data("data1", "val2");
throw ex;
```

```
${exception:format=toString,Data}
```

### Log full with inner exceptions

max 10 depth

```
${exception:format=toString,Data:maxInnerExceptionLevel=10}
```


## More Info and Examples
For more information, see [How to properly log exceptions](How-to-log-exceptions).

Writes log messages to the console. 

Supported in .NET, Silverlight, Compact Framework and Mono

## Configuration Syntax
```xml
<targets>
  <target xsi:type="Console"
          name="String"
          layout="Layout"
          footer="Layout"
          header="Layout"
          encoding="Encoding"
          error="Boolean"
          detectConsoleAvailable="Boolean" />
</targets>
```
Read more about using the [Configuration File](Configuration file).

## Parameters
### General Options
* **name** - Name of the target.

### Layout Options
* **layout** - Text to be rendered. [Layout](Layouts) Required. Default: `${longdate}|${level:uppercase=true}|${logger}|${message}`
* **footer** - Footer. [Layout](Layouts)  
* **header** - Header. [Layout](Layouts)

### Performance Options
* **OptimizeBufferReuse** - Reduce logging overhead, by allowing buffer reuse. Default: `True`
  > Introduced with NLog v4.4.2. Default became `True` until NLog v4.5

### Console Options
* **encoding** - File encoding name like "utf-8", "ascii" or "utf-16". See [Encoding class on MSDN](http://msdn.microsoft.com/en-us/library/system.text.encoding%28v=vs.110%29.aspx). Defaults to `Encoding.Default` (`UTF-8` on silverlight). Starting for NLog 4.0.

* **error** - Indicates whether to send the log messages to the standard error instead of the standard output. [Boolean](Data types) Default: `false`

* **detectConsoleAvailable** - Indicates whether the console target should disable itself when no console detected. [Boolean](Data types) Default: `false` (introduced in 4.3.10 with default: `true`. Since NLog 4.4 default `false`)
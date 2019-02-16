Provides fallback-on-error. 

Supported in .NET, Silverlight, Compact Framework and Mono.

## Configuration Syntax
```xml
<targets>
  <target xsi:type="FallbackGroup" name="String" returnToFirstOnSuccess="Boolean">
    <target xsi:type="wrappedTargetType" ... />
    <target xsi:type="wrappedTargetType" ... />
    ...
    <target xsi:type="wrappedTargetType" ... />
  </target>
</targets>
```

## Parameters
### General Options
* **name** - Name of the target.

### Fallback Options
* **returnToFirstOnSuccess** - Indicates whether to return to the first target after any successful write. `Boolean`. Default `false`

### Performance Options
* **OptimizeBufferReuse** - Reduce logging overhead, by allowing buffer reuse. Default: `True`
  > Introduced with NLog v4.4.2. Default became `True` with NLog v4.5

## Example

Fallback to another mail if the mailserver is down

```xml
<target xsi:type="FallbackGroup" 
        name="mail"
        returnToFirstOnSuccess="true">
    <target xsi:type="Mail"
            name="mailserver1"
            subject="Layout"
            to="Layout"
            from="Layout"
            smtpServer="mx1.example.com" 
            smtpPort="Integer"
            layout="Layout" />
    <target xsi:type="Mail"
            name="mailserver2" 
            subject="Layout"
            to="Layout"
            from="Layout"
            smtpServer="mx2.example.com" 
            smtpPort="Integer"
            layout="Layout" />
</target>
<rules>
  <logger name="*" minlevel="Trace" writeTo="mail" />
</rules>
```
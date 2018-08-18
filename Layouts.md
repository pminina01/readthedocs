Layouts are one of the attributes of most [targets](Targets). The layout attribute is used to determine the format of the information to be logged. Many pre-defined 'macros' or [Layout renderers](Layout-renderers) exist. In the below example `${machinename}` is an example of a layout renderer.

## Default Layout

If a target has the layout attribute, you may define a custom layout. If you do not specify a layout, the default layout is used. The default layout is:
```
${longdate}|${level:uppercase=true}|${logger}|${message}
```

## Pre-Defined Layouts

Several pre-defined layouts exist:


All layouts could be found here: http://nlog-project.org/config/?tab=layouts

## Example

An example of a simple layout looks like:
```
layout="${machinename} ${message}"
```

This layout is used in the NLog.config file like:
```xml
<?xml version="1.0" encoding="utf-8" ?>
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd" 
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

    <targets>
        <target name="console" xsi:type="ColoredConsole" 
                layout="${machinename} ${message}"/>
    </targets>

    <rules>
        <logger name="*" minlevel="Trace" writeTo="console" />
    </rules>
</nlog>
```
Value from the App Settings configuration 

From NLog 3.0+, in NLog.Extended

##Configuration Syntax
```
${appsetting:name=String:default=String}
```

##Parameters
###Rendering Options
* **name** - Key in the apps setting. Required.
* **Default** - Default value if not present. Optional.

##Example
Example .config

```xml
<configuration>
    <appSettings>
        <add key="MyKey" value="MyApplication" />
    </appSettings>
</configuration>
```

Example renderer: produces `MyApplication` is this case.
```
${appsetting:name=MyKey:default=mydefault}
```

Example#2 renderer: produces `mydefault` is this case.
```
${appsetting:name=MyKey2:default=mydefault}
```
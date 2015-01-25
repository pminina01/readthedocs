Value from the App Settings configuration 

From NLog 3.0+

##Configuration Syntax
Example renderer: produces `mydefault` if `MyKey` is not configured.
```
${appsetting:name=MyKey:default=mydefault}
```
Example .config

```xml
<configuration>
    <appSettings>
        <add key="MyKey" value="MyApplication" />
    </appSettings>
</configuration>
```

##Parameters
###Rendering Options
* **name** - Key in the apps setting. Required.
* **Default** - Default value if not present. Optional.
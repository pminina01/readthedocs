Render a NLog variable. The variable value can be set from the XML config and/or the API. 

Introduced in 4.1, seen [news post](http://nlog-project.org/2015/08/31/nlog-4-1-0-is-now-available.html) 

## Configuration Syntax
```
${var:name=String:default=String}
```

## Parameters

* **name** - Name of the NLog variable. Required.
* **default** - Default value to be used when the variable is not set.
Not used if _name_ is `null`

## Example

```xml
<nlog>
  <variable name="user" value="admin" />
  <variable name="password" value="realgoodpassword" />      
  <targets>
    <target name="debug" type="Debug" layout="${message} and ${var:user}=${var:password}" />
  </targets>
  <rules>
    <logger name="*" minlevel="Debug" writeTo="debug" />
  </rules>
</nlog>
```

### API

```c#
// create or edit
LogManager.Configuration.Variables["user"] = "admin";
LogManager.Configuration.Variables["password"] = "123";
// or remove
LogManager.Configuration.Variables.Remove("password");
```

## Notes
* Variables can be changed, deleted and created from the API
* A default value can be configured for a variable, e.g. `${var:password:default=unknown}`
* The old variables can still be used and so this is completely backwards-compatible.
* the `<variable>` is optional if no default is needed
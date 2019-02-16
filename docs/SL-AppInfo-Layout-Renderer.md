Information about Silverlight application. 

Supported in Silverlight.

## Configuration Syntax
```
${sl-appinfo:option=Enum}
```

## Parameters
### Rendering Options
* **option** - Specific information to display. Default: 0  
  Possible values:
  * _HasElevatedPermissions_ - Whether application is running with elevated permissions.
    
    > This parameter is not supported in:
    > * NLog v2.0 for Silverlight 2.0
    > * NLog v2.0 for Silverlight 3.0

  * _InstallState_ - Installed state of an application.

    > This parameter is not supported in:
    > * NLog v2.0 for Silverlight 2.0

  * _IsOutOfBrowser_ - Whether application is running out-of-browser.

    > This parameter is not supported in:
    > * NLog v2.0 for Silverlight 2.0

  * _XapUri_ - URI of the current application XAP file.
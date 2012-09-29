Information about Silverlight application. 

Supported in Silverlight.

##Configuration Syntax
```
${sl-appinfo:option=Enum}
```

##Parameters
###Rendering Options
* _option_ - Specific information to display. Default: 0  
  Possible values:
  * **HasElevatedPermissions** - Whether application is running with elevated permissions.
    
    > This parameter is not supported in:
    > * NLog v2.0 for Silverlight 2.0
    > * NLog v2.0 for Silverlight 3.0

  * **InstallState** - Installed state of an application.

    > This parameter is not supported in:
    > * NLog v2.0 for Silverlight 2.0

  * **IsOutOfBrowser** - Whether application is running out-of-browser.

    > This parameter is not supported in:
    > * NLog v2.0 for Silverlight 2.0

  * **XapUri** - URI of the current application XAP file.
A value from the Registry. 

Supported in .NET, Compact Framework and Mono.

##Configuration Syntax
```
${registry:value=String:key=String:defaultValue=String}
```

##Parameters
###Registry Options
* _value_ - Registry value name.
* _key_ - Registry key. Required.  
  Must have one of the forms:  
  * HKLM\Key\Full\Name
  * HKEY_LOCAL_MACHINE\Key\Full\Name
  * HKCU\Key\Full\Name
  * HKEY_CURRENT_USER\Key\Full\Name
defaultValue - Value to be output when the specified registry key or value is not found.
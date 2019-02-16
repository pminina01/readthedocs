A value from the Registry. 

Supported in .NET, Compact Framework and Mono.

## Configuration Syntax
```
${registry:value=Layout:key=Layout:defaultValue=Layout:view=enum:requireEscapingSlashesInDefaultValue=boolean}
```

## Parameters
### Registry Options
* **value** - Registry value name. Since NLog 4.3 a `Layout`. Before `String`.
* **key** - Registry key. Required. Since NLog 4.3 a `Layout`. Before `String`.
  Must have the form: _hive_/key/subkey/name
  Possible hives: HKLM/HKEY_LOCAL_MACHINE/HKCU/HKEY_CURRENT_USER
  Also possible since NLog 4.3: HKEY_CLASSES_ROOT/HKEY_USERS/HKEY_CURRENT_CONFIG/HKEY_DYN_DATA/HKEY_PERFORMANCE_DATA
   
* **defaultValue** - Value to be output when the specified registry key or value is not found. Since NLog 4.3 a `Layout`. Before `String`.
* **RequireEscapingSlashesInDefaultValue** - Introduced in NLog 4.3 `boolean`. Require escaping backward slashes in `DefaultValue`. Need to be backwardscompatible. Default `true`. Will be removed in the future. 
* **View** - Introduced in NLog 4.3 . Registry32, Registry64, Default 
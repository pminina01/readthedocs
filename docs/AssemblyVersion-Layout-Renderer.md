Renders assembly version information from the entry assembly or a named assembly.

Supported in .NET, Silverlight, Compact Framework and Mono. Introduced for ASP.NET / ASP.NET Core in NLog.Web 4.5.0 / NLog.Web.AspNetCore 4.4.0.

## Configuration Syntax
```
${assembly-version:name=string:type=Enum}
```
## Parameters

* **name** - Display name of the assembly to retrieve a version from, as determined by its `FullName` property. The assembly will be loaded if needed. If not specified, will use the entry assembly (this did not function correctly for .NET Core until NLog.Web.AspNetCore 4.6). Introduced in NLog 4.3.7.

* **type** - Type of the assembly version value to retrieve. Default: `Assembly`. Introduced in NLog 4.5. For ASP.NET, introduced in NLog.Web / NLog.Web.AspNetCore 4.6.

  Possible values:
  * **Assembly** - Assembly version. Value for `AssemblyVersion` attribute.

    Note: UWP earlier than .NET Standard 1.5 uses value for `ApplicationVersion`

  * **File** - File version. Value for `AssemblyFileVersion` attribute.

    Notes:
    - UWP earlier than .NET Standard 1.5 uses Assembly instead unless a value is given for the `name` parameter
    - Silverlight always uses Assembly

  * **Informational** - Additional version information. Value for `AssemblyInformationalVersion` attribute.

    Notes:
    - UWP earlier than .NET Standard 1.5 uses Assembly instead unless a value is given for the `name` parameter
    - Silverlight always uses Assembly


## Examples

Retrieve assembly version for entry assembly:
```
${assembly-version}
```

Retrieve assembly version for assembly name `NLogAutloadExtension`:
```
${assembly-version:NLogAutloadExtension}
```

Retrieve file version for entry assembly:
```
${assembly-version:type=File}
```

Retrieve informational version for assembly name `NLogAutloadExtension`:
```
${assembly-version:name=NLogAutloadExtension:type=Informational}
```

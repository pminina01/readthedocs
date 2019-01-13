The NetBIOS Machine name that the process is running on. 

Supported in .NET and Mono.

## Configuration Syntax
```
${machinename}
```

## Remarks
NetBIOS name is limited to MAX_COMPUTERNAME_LENGTH which is 15 for Windows.

[${hostname}](HostName-Layout-Renderer) has support for the full DNS-name.
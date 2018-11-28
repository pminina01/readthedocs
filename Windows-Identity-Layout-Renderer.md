Thread Windows identity information (username). 

Supported in .NET and Mono.

---
 ℹ️  For .NET Core 2.1 Console application you need install the `NLog.WindowsIdentity` package and include it
to `<extensions>` tag in `nlog.config`.

---

## Configuration Syntax
```
${windows-identity:userName=Boolean:domain=Boolean}
```

## Parameters
### Rendering Options
* **userName** - Indicates whether username should be included. Boolean Default: True
* **domain** - Indicates whether domain name should be included. Boolean Default: True
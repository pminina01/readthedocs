Impersonates another user for the duration of the write. 

Supported in .NET and Mono

## Configuration Syntax
```
<targets>
  <target xsi:type="ImpersonatingWrapper"
          name="String"
          userName="String"
          password="String"
          revertToSelf="Boolean"
          impersonationLevel="Enum"
          domain="String"
          logOnType="Enum"
          logOnProvider="Enum">
    <target xsi:type="wrappedTargetType" ...target properties... />
  </target>
</targets>
```
## Parameters
### General Options
* **name** - Name of the target.

### Impersonation Options
* **userName** - Username to change context to.

* **password** - User account password.

* **revertToSelf** - Indicates whether to revert to the credentials of the process instead of impersonating another user. Boolean Default: False
 
* **impersonationLevel** - Required impersonation level.  
Possible values:  
  * Anonymous - Anonymous Level.
  * Delegation - Delegation Level.
  * Identification - Identification Level.
  * Impersonation - Impersonation Level.

* **domain** - Windows domain name to change context to. Default: .

* **logOnType** - Logon Type.  
Possible values:  
  * Batch - Batch Logon.
  * Interactive - Interactive Logon.
  * Network - Network Logon.
  * NetworkClearText - Network Clear Text Logon.
  * NewCredentials - New Network Credentials.
  * Service - Logon as a Service.

* **logOnProvider** - Type of the logon provider.  
Possible values:  
 * Default - Use the standard logon provider for the system.
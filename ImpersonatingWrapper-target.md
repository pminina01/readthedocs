Impersonates another user for the duration of the write. 

Supported in .NET and Mono
##Configuration Syntax
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
##Parameters
###General Options
_name_ - Name of the target.
###Impersonation Options
_userName_ - Username to change context to.

_password_ - User account password.

_revertToSelf_ - Indicates whether to revert to the credentials of the process instead of impersonating another user. Boolean Default: False
 
 _impersonationLevel_ - Required impersonation level.  
Possible values:  
* Anonymous - Anonymous Level.
* Delegation - Delegation Level.
* Identification - Identification Level.
* Impersonation - Impersonation Level.

_domain_ - Windows domain name to change context to. Default: .

_logOnType_ - Logon Type.  
Possible values:  
* Batch - Batch Logon.
* Interactive - Interactive Logon.
* Network - Network Logon.
* NetworkClearText - Network Clear Text Logon.
* NewCredentials - New Network Credentials.
* Service - Logon as a Service.

_logOnProvider_ - Type of the logon provider.  
Possible values:  
* Default - Use the standard logon provider for the system.
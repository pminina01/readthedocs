Sends log messages by email using SMTP protocol. 

Combines well with [FallbackGroup Target](https://github.com/NLog/NLog/wiki/FallbackGroup-target) in order to create a fallback with multiple SMTP Hosts, example see [here](https://github.com/NLog/NLog/wiki/Mail-target#mail-target-wrapped-by-fallbackgroup-target).

Supported in .NET and Mono
##Configuration Syntax
```xml
<targets>
  <target xsi:type="Mail"
          name="String"
          header="Layout"
          footer="Layout"
          layout="Layout"
          html="Boolean"
          addNewLines="Boolean"
          replaceNewlineWithBrTagInHtml="Boolean"
          encoding="Encoding"
          subject="Layout"
          to="Layout"
          bcc="Layout"
          cc="Layout"
          from="Layout"
          body="Layout"
          smtpUserName="Layout"
          enableSsl="Boolean"
          smtpPassword="Layout"
          smtpAuthentication="Enum"
          smtpServer="Layout"
          smtpPort="Integer"
          useSystemNetMailSettings="Boolean"
          deliveryMethod="Enum"
          pickupDirectoryLocation="String"
          timeout="Integer" />
</targets>
```
Read more about using the [Configuration File](Configuration file).
##Parameters
###General Options
_name_ - Name of the target.
###Layout Options
_header_ - Header. [Layout](Data-types)

_footer_ - Footer. [Layout](Data-types)

_layout_ - Text to be rendered. [Layout](Data-types) Required. Default: `${message}${newline}`. Same as _body_ property

_html_ - Indicates whether to send message as HTML instead of plain text. [Boolean](Data-types) Default: `false`

_addNewLines_ - Indicates whether to add new lines between log entries. [Boolean](Data-types)

_replaceNewlineWithBrTagInHtml_ - Indicates whether NewLine characters in the body should be replaced with `<br/>` tags. [Boolean](Data-types) Default: `false`

_encoding_ - Encoding to be used for sending e-mail. [Encoding](Data-types) Default: `UTF-8`
###Message Options
_subject_ - Mail subject. [Layout](Data-types) Required. Default: Message from NLog on ${machinename}

_to_ - Recipients' email addresses separated by semicolons (e.g. john@domain.com;jane@domain.com). [Layout](Data-types). Starting in NLog 4.0 this field is no longer required, but To, BCC or CC should be defined otherwise an exception is thrown. 

_bcc_ - BCC email addresses separated by semicolons (e.g. john@domain.com;jane@domain.com). [Layout](Data-types)

_cc_ - CC email addresses separated by semicolons (e.g. john@domain.com;jane@domain.com). [Layout](Data-types)

_from_ - Sender's email address (e.g. joe@domain.com). [Layout](Data-types) Required.

_body_ - Same as _Layout_ property. Mail message body (repeated for each log message send in one mail). [Layout](Data-types) Default: `${message}${newline}` 

###SMTP Options
_smtpUserName_ - Username used to connect to SMTP server (used when SmtpAuthentication is set to "basic"). [Layout](Data-types)

_enableSsl_ - Indicates whether SSL (secure sockets layer) should be used when communicating with SMTP server. [Boolean](Data-types) Default: False  

_smtpPassword_ - Password used to authenticate against SMTP server (used when SmtpAuthentication is set to "basic"). [Layout](Data-types)

_smtpAuthentication_ - SMTP Authentication mode. Default: None  
Possible values:
* Basic - Basic - username and password.
* None - No authentication.
* Ntlm - NTLM Authentication.

_smtpServer_ - SMTP Server to be used for sending. [Layout](Data-types) Required.

_smtpPort_ - Port number that SMTP Server is listening on. [Integer](Data-types) Default: 25

_useSystemNetMailSettings_ - Force using smtp configuration from system.net/mailSettings. [Boolean](Data-types) Default: False

_timeout_ - Indicates the SMTP client timeout. [Integer](Data-types) Default: 10000

_pickupDirectoryLocation_ - Gets or sets the folder where applications save mail messages to be processed by the local SMTP server (__introduced in NLog 4.2__).

_smtpDeliveryMethod_ - Specifies how outgoing email messages will be handled (__introduced in NLog 4.2__). Default: Network 
Possible values:
* Network - Email is sent through the network to an SMTP server.
* PickupDirectoryFromIis - Email is copied to the pickup directory used by a local Internet Information Services (IIS) for delivery.
* SpecifiedPickupDirectory - Email is copied to the directory specified by the PickupDirectoryLocation property for delivery by an external application.
##Remarks

### Application Configuration File
If the application config file contains mail settings, fx.:

```xml
<system.net>
  <mailSettings>
    <smtp from="mail@domain.com" deliveryMethod="SpecifiedPickupDirectory">
      <network host="localhost" port="25"/>
      <specifiedPickupDirectory pickupDirectoryLocation="C:/Temp/Email"/>
    </smtp>
  </mailSettings>
</system.net>
```

These values will be used, if target doesn't override them (see _useSystemNetMailSettings_ attribute).

### Email Address Format

It is possible to use an address in format "John Doe &lt;john.doe@example.com&gt;" but the special characters < and > must be escaped. The result would be `John Doe &lt;john.doe@example.com&gt;`


### Mail Target wrapped by FallbackGroup Target

Example configuration for a Mailserver Fallback with multiple hosts.

```xml
<target xsi:type="FallbackGroup" 
        name="mail"
        returnToFirstOnSuccess="true">
    <target xsi:type="Mail"
            name="mailserver1"
            subject="Layout"
            to="Layout"
            from="Layout"
            smtpServer="mx1.example.com" 
            smtpPort="Integer"
            layout="Layout" />
    <target xsi:type="Mail"
            name="mailserver2" 
            subject="Layout"
            to="Layout"
            from="Layout"
            smtpServer="mx2.example.com" 
            smtpPort="Integer"
            layout="Layout" />
</target>
```
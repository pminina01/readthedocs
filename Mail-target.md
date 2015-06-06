Sends log messages by email using SMTP protocol. 

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
> This parameter is not supported in:
> * NLog v1.0 for .NET Framework 1.0
> * NLog v1.0 for .NET Framework 1.1
> * NLog v1.0 for .NET Framework 2.0

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
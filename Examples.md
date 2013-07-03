##Using NLog with GMail
In order to use [Mail target](Mail-target) with GMail, you need to use the following server configuration:
```
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

  <targets>
    <target name="gmail" xsi:type="Mail"
            smtpServer="smtp.gmail.com"
            smtpPort="587"
            smtpAuthentication="Basic"
            smtpUsername="user@gmail.com"
            smtpPassword="password"
            enableSsl="true"
            from="emailaddress@gmail.com"
            to="recipient@example.com"
            cc="alice@example.com;bob@example.com;charlie@example.com"
          />
  </targets>

  <rules>
    <logger name="*" minlevel="Debug" writeTo="gmail" />
  </rules>
</nlog>
```
(Note that this is only supported in NLog 2.0 and higher, because NLog 1.0 does not support **enableSsl** parameter).

##Using NLog with Growl for Windows
[Ryan Farley](http://ryanfarley.com/blog/articles/about.aspx) has a great article on [how to use NLog with Growl for Windows](http://ryanfarley.com/blog/archive/2010/05/06/announcing-the-growl-for-windows-target-for-nlog.aspx)
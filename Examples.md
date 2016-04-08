##Using NLog with GMail
In order to use [Mail target](Mail-target) with GMail, you need to use the following server configuration:
```xml
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

  <targets>
    <target name="gmail" xsi:type="Mail"
            smtpServer="smtp.gmail.com"
            smtpPort="587"
            smtpAuthentication="Basic"
            smtpUserName="user@gmail.com"
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

##Using NLog with Growl for Windows
[Ryan Farley](http://ryanfarley.com/blog/articles/about.aspx) has a great article on [how to use NLog with Growl for Windows](http://ryanfarley.com/blog/archive/2010/05/06/announcing-the-growl-for-windows-target-for-nlog.aspx)

##Changing log file name at runtime

```c#
using NLog.Targets;
...
FileTarget target = LogManager.Configuration.FindTargetByName(targetName) as FileTarget;
target.FileName = filename;
```

Note that it is often easier to create the file name with a combination of [Layout-Renderers](layout renderers).
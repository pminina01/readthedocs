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
FileTarget target = LogManager.Configuration.FindTargetByName<FileTarget>(targetName);
target.FileName = filename;
```

Note that it is often easier to create the file name with a combination of [Layout-Renderers](layout renderers).


## Using NLog with [Autofac](https://autofac.org/) - [APS.NET Web API 2](http://www.asp.net/web-api)

This example is using a nuget package [Autofac.Extras.Nlog](https://www.nuget.org/packages/Autofac.Extras.NLog) that takes care of creating the [Autofac module](http://autofac.readthedocs.io/en/latest/configuration/modules.html) needed to wire up the dependency in the Web API.

First, add an nlog section to the configSections in the Web.config:

```xml
  <configSections>
    <section name="nlog" type="NLog.Config.ConfigSectionHandler, NLog" />
  </configSections>
```
Then, in the Global.asax.cs (or Startup.cs, depending where Autofac is configured) register the module provided by the Autofac.Extras.Nlog nuget package:

```c#
  var builder = new ContainerBuilder();
   ...

  builder.RegisterModule<NLogModule>();
```
Nothing extra is needed to configure the [NLog targets](https://github.com/nlog/nlog/wiki/Targets).

This example uses constructor injection but Autofac.Extras.Nlog supports property and service locator injection as well.

```c#
using System;
using System.Net;
using System.Net.Http;
using System.Threading.Tasks;
using Autofac.Extras.NLog;
using Microsoft.AspNet.Identity;

    public class UserService: IUserService
    {
        private readonly IUserStore _userStore;
        private readonly ILogger _logger;

        public UserService(IUserStore userStore, ILogger logger)
        {
            _userStore = userStore;
            _logger = logger;
        }

        .....
    }
```

Happy logging!

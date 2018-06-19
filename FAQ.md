* **What is NLog?**
  - NLog is a free and open source library which helps to write log messages. 

* **Why should I use a log library? I can just do `file.WriteLine()`**
  - Beside writing to files, you can write to many different targets, like databases, event viewer, trace etc. 
  - The output is templatable with many predefined template values. 
  - With a simple configuration file you can decide runtime (after deployment), what to log and where! No need to restart the program or recyle the app pool!

* **Why should I use NLog?**
  - NLog is fully written in C#, has many years of experience and is easy to extend!

* **Is it free?**
  - Yes, it's licensed under the BSD license, so you can use it in commercial (closed source) programs without problems. 
  
* **Show me the magic!**
  - Check the [tutorial](https://github.com/NLog/NLog/wiki/Tutorial) to get started!
 
* **Just show me a config example**
  - [voilà](https://github.com/NLog/NLog/wiki/NLog-config-Example)
  

* **I can't see anything?!**
  - NLog not working as expected? Check the [troubleshooting guide](https://github.com/NLog/NLog/wiki/Logging-troubleshooting). If you think it's a bug, please check [contributing.md](https://github.com/NLog/NLog/blob/master/CONTRIBUTING.md#bug-reports]) and [create a GitHub issue](https://github.com/NLog/NLog/issues/new)!

* **I'm missing important stuff!**
  - You can send a feature request, but do you know you can [extend NLog with a few lines of code](http://nlog-project.org/2015/06/30/extending-nlog-is-easy.html)?

* **I'm missing the trace and debug logs in ASP.NET Core 2**

  -  [Check your appsettings.json](https://github.com/NLog/NLog.Web/wiki/Missing-trace%5Cdebug-logs-in-ASP.NET-Core-2%3F)


* **How do I upgrade to NLog 4.x?** 
  - Check the [4.0 release post](http://nlog-project.org/2015/06/09/nlog-4-has-been-released.html), there are some breaking changes.
  - Update all the NLog packages. The latest stable version is recommend. 
  - When upgrading from NLog 4.1.0, please the next question.

* **I have trouble updating NLog from 4.1.0**
  - We take [semver](https://semver.org) very serious! Because NLog is strong named, it's important to keep the assembly version of all major versions the same, otherwise every library build on 4.0.0 should be reompiled for every other 4.x release (4.1, 4.2 etc)  - which is unwanted because of semver. <br>
   In NLog 4.1.0 there was a mistake in the assembly version, which has been fixed in 4.1.1. Upgrading from NLog 4.1.0 to another version can give issues when using NuGet. This will result in the following error:
   
  > Could not load file or assembly 'NLog' or one of its dependencies. The located assembly's manifest definition does not match the assembly reference. (Exception from HRESULT: 0x80131040)

  If you upgrade, remove or alter the `<assemblybinding>`, as explained at the [4.1.1 news post](http://nlog-project.org/2015/09/12/nlog-4-1-1-has-been-released.html).    
  
* **Should I use Common Logging?**
   - That's up to you. It has it pros and cons. The greatest advantage is that you can easily switch between logging implementations (NLog, Log4Net, EntLib). This can be very important if you’re writing a library yourself, then the user who's using your library can choose which implementation to use.

  - There are some downsides: 

     - You are limited in some features, or some features aren't available at all (like context classes or event properties)
     - The performance is a bit lower.
     - The platform support is lower. For example, there is no Xamarin support or a specialized .Net 4.5 build
     - The progress is limited by NLog and Common logging. 
  
* **Which Common Logging version should I use?**
   - As you may have noticed the latest version of Common Logging doesn't match the latest version of NLog -  the latest Common Logging is build to NLog 4.1. But that is not a problem! Since NLog 4.0 the assembly version is fixed to `4.0.0.0` and because follow [semver](https://semver.org), you can use the latest version of NLog with [Common.Logging.NLog41](https://www.nuget.org/packages/Common.Logging.NLog41/). 
    
* **I'm writing a library who's using NLog. Should I update when NLog has an update?**
   - If you don't use the latest additions, then you should only update every NLog major version. As mentioned at the Common Logging version, we will keep the assembly version fixed. The end-user don't need `<assemblybinding>`-magic! So in short: your library should target NLog 4.0 and in the future NLog 5.0.

* [Logging is not working - how to troubleshoot?](Logging-troubleshooting)
* [How to properly log exceptions?](How-to-log-exceptions)
* [How to configure logging in a component?](Configure-component-logging)
* [How do I get the most optimal performance?](performance)
* [How do I writing custom Targets, layouts and layout renderers?](Extending%20NLog)
* [How to load NLog configuration from non standard path](Explicit-NLog-configuration-loading)
* [How could I combine programmatic configuration with XML configuration?](Combine-XML-config-with-C%23-config)
* [How to create Logger for sub classes](How-to-create-Logger-for-sub-classes)
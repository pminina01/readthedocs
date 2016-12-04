Before you could use your custom layout, layout renderer, target or condition, you have to register it. You have the following options:

## Separate DLL and auto register (non .NET Core)
Introduced in NLog 4.0, and not working yet for .NET Core. Also from the GAC this won't work.

Name your assembly "NLog*.dll", like “NLog.CustomTarget.dll”. When the assembly is in the same folder as nlog.dll, it will be autoloaded when the configuration changes. You could hot-swap those NLog extensions. 

## Separate DLL and `<extensions>`

This works for .NET Core and the GAC. 

Include your assembly with the `<extensions>` syntax. Use the assembly name (not the filename)

```xml
<nlog> 
  <extensions> 
    <add assembly="MyAssembly"/> 
  </extensions> 
```

## Manual register

Register manually your extension.

Short syntax introducted in NLog 4.4
```c#
//target
Target.Register<MyNamespace.MyFirstTarget>("MyFirst"); //generic
Target.Register("MyFirst", typeof(MyNamespace.MyFirstTarget)); //OR, dynamic

//layout renderer
LayoutRenderer.Register<MyNamespace.MyFirstLayoutRenderer>("MyFirst"); //generic
LayoutRenderer.Register("MyFirst", typeof(MyNamespace.MyFirstLayoutRenderer)); //dynamic

//layout
Layout.Register<MyNamespace.MyFirstLayout>("MyFirst"); //generic
Layout.Register("MyFirst", typeof(MyNamespace.MyFirstLayout)); //dynamic

Older syntax, still supported

```c#
//target
ConfigurationItemFactory.Default.Targets
                            .RegisterDefinition("MyFirst", typeof(MyNamespace.MyFirstTarget));

//layout renderer
ConfigurationItemFactory.Default.LayoutRenderers
                            .RegisterDefinition("hello-world", typeof(MyNamespace.HelloWorldLayoutRenderer));

//layout 
ConfigurationItemFactory.Default.Layouts
                            .RegisterDefinition("csv", typeof(MyNamespace.CsvLayout));


```


 
Example with a `<include />` and  `<variable />` in the XML config


## base file: d:\nlog-file.config

File to be included. 
Contains one target and needs `${productName}`

```xml
<?xml version="1.0" encoding="utf-8" ?>
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <!-- This file will be included. -->
  <!--  Note: Attributes on the "nlog" element are ignored for this file, the ones of the main config will be used. -->

  <!-- the variable ${productName} must be defined in the main nlog.config -->
  
  <targets>
  
          <target name="file1" xsi:type="File" fileName="D:\logs\${productName}\${shortdate}.log" 
          layout="${time} [${level:uppercase=true}] |${logger}| ${message} ${exception}|"/>
  </targets>
  
</nlog>

```



## nlog.config
The main file. 
e.g. in the root folder of your application. Contains in this example no targets, only `<include />, `<logger />`, `<variable />`


```xml

<?xml version="1.0" encoding="utf-8" ?>
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd"      
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      autoReload="true"   
      internalLogLevel="Off" >
               
  <variable name="productName" value="myProduct"/> <!-- override productName in includes -->
                           
  <include file="D:\nlog-file.config"/>    
   
  <variable name="myVar" value="myValue"/> <!-- note: will be set after the 2 includes are loaded -->
     
  <rules>      
    <logger name="*" minlevel="Info" writeTo="file1" enabled="false" />     
    <logger name="PerformanceLogger" minlevel="Trace"  writeTo="file1" enabled="false">   <!-- not enabled, only when tracing -->
    </logger> 
  </rules>
</nlog>

```

Calls the specified web service on each log message. 

Supported in .NET, Silverlight, Compact Framework and Mono.

## Configuration Syntax
```xml
<targets>
  <target xsi:type="WebService"
          name="String"
          url="System.Uri"
          encoding="Encoding"
          includeBOM="Nullable boolean"
          protocol="Enum"
          namespace="String"
          methodName="String"
          preAuthenticate="Boolean">
    <parameter name="String" layout="Layout" type="System.Type"/><!-- repeated -->
    <header name="String" layout="Layout"/><!-- repeated -->
  </target>
</targets>
```

## Parameters
### General Options
* **name** - Name of the target.

### Parameter Options
* **parameters** - The array of parameters to be passed. Collection  
Each collection item is represented by `<parameter />` element with the following attributes:  
  * **name** - Name of the parameter.
  * **layout** - Layout that should be use to calculate the value for the parameter. Layout Required.
  * **type** - Type of the parameter. System.Type

### Header Options
* **headers** - The array of Http-headers to be passed. Collection
Each collection item is represented by `<header />` element with the following attributes:  
  * **name** - Name of the header parameter.
  * **layout** - Layout that should be use to calculate the value for the parameter. Layout Required.


### Web Service Options
* **url** - Web service URL. System.Uri

* **encoding** - Encoding. Encoding name like "utf-8", "ascii" or "utf-16". See [Encoding class on MSDN](http://msdn.microsoft.com/en-us/library/system.text.encoding%28v=vs.110%29.aspx)

* **includeBOM** - Skip or add Byte-order-mark (BOM) for UTF-8. Only used if encoding is set to UTF-8, because a BOM is optional in UTF-8.  default: `false`. For more info on BOM, check [Wikipedia](https://en.wikipedia.org/wiki/Byte_order_mark).
Possible options: 
  - `null`: doesn’t change BOM. 
  - `true`: always include UTF-8 BOM UTF-8 encodings. 
  - `false`: default, always skip BOM on UTF-8 encodings.

* **escapeDataRfc3986** - NLog will by default encode parameters as UTF8 and escape special characters according to Rfc2396. To escape data according to standard Rc3986, set this option to 'true' (Available from NLog 4.4)

* **escapeDataNLogLegacy** - NLog will by default encode parameters as UTF8 and escape special characters according to Rfc2396. To escape data according to the old non-standard NLog style, set this option to 'true' (Available from NLog 4.4)

* **protocol** - Protocol to be used when calling web service. Default: Soap11  
Possible values:  
  * JsonPost - JSON POST  - introduced in NLog 4.4 - ContentType "application/json"
  * XmlPost - XML POST - introduced in NLog 4.4 -  ContentType "application/xml"
  * HttpGet - Use HTTP GET Protocol.
  * HttpPost - Use HTTP POST Protocol.  ContentType "application/x-www-form-urlencoded"
  * Soap11 - Use SOAP 1.1 Protocol.
  * Soap12 - Use SOAP 1.2 Protocol.

* **namespace** - Web service namespace.

* **methodName** - Web service method name.

* **PreAuthenticate** - Indicates whether to pre-authenticate the HttpWebRequest (Requires 'Authorization' in **Headers** parameters)

* **

* **ProxyType** - Configuration of HttpWebRequest.Proxy. Default: DefaultWebProxy (Introduced with NLog 4.5)  
Possible values:
  * DefaultWebProxy - Default proxy configuration from WebRequest.DefaultWebProxy (defaultProxy in app.config)
  * AutoProxy - WebRequest.GetSystemWebProxy() with default network credentials.
  * ProxyAddress - User defined proxy address retrieved the ProxyAddress parameter.
  * NoProxy - Disables use of proxy (fast)

* **ProxyAddress** - User defined proxy address, include port separated by a colon (Introduced with NLog 4.5) 

## Remarks
The web service must implement a method that accepts a number of string parameters.

## Example

### Example config:

```xml
<nlog>
    <targets>
        <target type='WebService'
                name='ws'
                url='http://localhost:1234/logme'
                protocol='HttpPost'
                encoding='UTF-8'   >
            <parameter name='param1' type='System.String' layout='${message}'/> 
            <parameter name='param2' type='System.String' layout='${level}'/>
        </target>
    </targets>
    <rules>
      <logger name='*' writeTo='ws'></logger>
    </rules>
</nlog>
```

### Example API controller

```c#

public class LogMeController : ApiController
{
    /// <summary>
    /// We need a complex type for modelbinding because 
    /// of content-type: "application/x-www-form-urlencoded" 
    /// in <see cref="WebServiceTarget"/>
    /// </summary>
    public class ComplexType
    {
        public string Param1 { get; set; }
        public string Param2 { get; set; }
    }
    
    /// <summary>
    /// Post
    /// </summary>
    public void Post([FromBody] ComplexType complexType)
    {
        //do something
    }
}
```
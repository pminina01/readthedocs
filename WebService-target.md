Calls the specified web service on each log message. 

Supported in .NET, Silverlight, Compact Framework and Mono.
##Configuration Syntax
```xml
<targets>
  <target xsi:type="WebService"
          name="String"
          url="System.Uri"
          encoding="Encoding"
          includeBOM="Nullable boolean"
          protocol="Enum"
          namespace="String"
          methodName="String">
    <parameter layout="Layout" name="String" type="System.Type"/><!-- repeated -->
  </target>
</targets>
```
##Parameters
###General Options
_name_ - Name of the target.
###Parameter Options
_parameters_ - The array of parameters to be passed. Collection  
Each collection item is represented by \<parameter /> element with the following attributes:  
* _layout_ - Layout that should be use to calcuate the value for the parameter. Layout Required.
* _name_ - Name of the parameter.
* _type_ - Type of the parameter. System.Type

###Web Service Options
_url_ - Web service URL. System.Uri

_encoding_ - Encoding. Encoding name like "utf-8", "ascii" or "utf-16". See [Encoding class on MSDN](http://msdn.microsoft.com/en-us/library/system.text.encoding%28v=vs.110%29.aspx)

_includeBOM_ - Skip or add Byte-order-mark (BOM) for UTF-8. Only used if encoding is set to UTF-8, because a BOM is optional in UTF-8.  default: `false`. Possible options: 
  - `null`: doesn’t change BOM. 
  - `true`: always include UTF-8 BOM UTF-8 encodings. 
  - `false`: default, always skip BOM on UTF-8 encodings.

For more info on BOM, check [Wikipedia](https://en.wikipedia.org/wiki/Byte_order_mark)


_protocol_ - Protocol to be used when calling web service. Default: Soap11  
Possible values:  
* HttpGet - Use HTTP GET Protocol.
* HttpPost - Use HTTP POST Protocol.
* Soap11 - Use SOAP 1.1 Protocol.
* Soap12 - Use SOAP 1.2 Protocol.

_namespace_ - Web service namespace.

_methodName_ - Web service method name.

##Remarks
The web service must implement a method that accepts a number of string parameters.


##Example

Example config:

```xml
<nlog throwExceptions='true'>
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

Example API controller

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
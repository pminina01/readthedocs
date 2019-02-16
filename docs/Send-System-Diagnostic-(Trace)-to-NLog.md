Needed in your config:

```xml
  <system.diagnostics>
    <sources>
      <source name="System.ServiceModel.MessageLogging" switchValue="All">
        <listeners>
          <add name="nlog" />
        </listeners>
      </source>
    </sources>
    <trace autoflush="true" />    
    <sharedListeners>
      <add name="nlog" type="NLog.NLogTraceListener, NLog"  />
    </sharedListeners>
  </system.diagnostics>
```

and
```xml
  <system.serviceModel>
    <diagnostics>
        <messageLogging logEntireMessage="true"
                                    logMalformedMessages="true"
                                    logMessagesAtServiceLevel="true"
                                    logMessagesAtTransportLevel="true"
                        
                                    />
    </diagnostics>
    
  </system.serviceModel>
```
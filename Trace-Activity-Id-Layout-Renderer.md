Write the `System.Diagnostics` trace correlation id. 

Introduced in NLog v4.1.

Supported in .NET and Mono.

## Configuration Syntax
```xml
${activityid}
```

## Remarks

If the `Trace.CorrelationManager.ActivityId` is equal to `Guid.Empty`, then appends `String.Empty`, otherwise appends `Trace.CorrelationManager.ActivityId` as separated by hyphens according to the `CultureInfo.InvariantCulture`. 

## Example

For an ASP.Net WebAPI application, initialize the `Trace.CorrelationManager.ActivityId` in the `Global.asax`, `Application_BeginRequest` event:

`    protected void Application_BeginRequest(object sender, EventArgs e)`
    `{`
        `...`
        `Trace.CorrelationManager.ActivityId = new Guid();`
    `}`
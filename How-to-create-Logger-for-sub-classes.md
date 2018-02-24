When we wish to expose the logger into sub classes the following pattern could be used.

```csharp
class BaseClass
{
    protected BaseClass()
    {
        Log = LogManager.GetLogger(GetType().FullName);
    }

    protected Logger Log { get; private set; }
}

class ExactClass : BaseClass
{
    public ExactClass() : base() { }
    ...
}
```
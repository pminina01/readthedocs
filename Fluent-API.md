##Fluent API

Writing info message via fluent API.

    using NLog.Fluent;
    ...
    _logger.Info()
        .Message("This is a test fluent message '{0}'.", DateTime.Now.Ticks)
        .Property("Test", "InfoWrite")
        .Write();

Writing error message.

    try
    {
        string text = File.ReadAllText(path);
    }
    catch (Exception ex)
    {
        _logger.Error()
            .Message("Error reading file '{0}'.", path)
            .Exception(ex)
            .Property("Test", "ErrorWrite")
            .Write();
    }

##Caller Info

Use the static Log class so you don't have to include loggers in all of classes.  The static Log class using .net 4.5 caller info to get the logger from the file name. 

Writing info message via static Log class with fluent API.

    Log.Info()
        .Message("This is a test fluent message.")
        .Property("Test", "InfoWrite")
        .Write();

Writing error message.

    try
    {
        string text = File.ReadAllText(path);
    }
    catch (Exception ex)
    {
        Log.Error()
            .Message("Error reading file '{0}'.", path)
            .Exception(ex)
            .Property("Test", "ErrorWrite")
            .Write();
    }
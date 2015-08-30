Mapped Diagnostic Logical Context is the async version of the Mapped Diagnostics Context - a logical call context structure that keeps a dictionary of strings and provides methods to output them in layouts. Allows for maintaining state across asynchronous tasks and call contexts. Mostly for compatibility with log4net (log4net.ThreadLogicalContext).

Use the Mapped Diagnostic Logical Context when you have information that you want available to every logger executing on the current logical context.

Supported in .NET 4.0 and 4.5.
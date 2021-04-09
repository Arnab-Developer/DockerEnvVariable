# ASP.NET option pattern demo

This is a demo app to show the difference between `IOptionsMonitor`, `IOptions`
and `IOptionsSnapshot`.

- IOptionsMonitor: always return the new value
- IOptions: always return the old value until the app is restarted
- IOptionsSnapshot: return the new value if it is a new request

There are two action methods, `Index` and `Privacy`. Both the methods are having 
the same code in it which is getting the value of `Name `from `appsettings` for 
20 times in a loop using `IOptionsMonitor`, `IOptions` and `IOptionsSnapshot`.

```c#
for (int i = 0; i < 20; i++)
{
    string name1 = _optionsMonitor.CurrentValue.Name;
    string name2 = _options.Value.Name;
    string name3 = _optionsSnapshot.Value.Name;
}
```

If you put a breakpoint in the loop in the `Index` method and while the loop is 
executing, if you change the value of the `Name` in `appsettings` then you can able 
to see that `IOptionsMonitor` is returning the new value but `IOptions` and 
`IOptionsSnapshot` is returning the old value.

When redirect happens from `Index` to `Privacy` then a new request has been made
and now you can able to see `IOptionsSnapshot` is returning the new value like
`IOptionsMonitor` but `IOptions` is still returning the old value.

If you restart the app then you will able to see that `IOptions` is returning the
new value like `IOptionsMonitor` and `IOptionsSnapshot`.

For more information about ASP.NET option pattern, please read 
[this doc](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/configuration/options?view=aspnetcore-5.0).

## Tech stack

Visual Studio 2019 and ASP.NET 5
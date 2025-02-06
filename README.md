# Oneiro AspNetCore LanguageExt

Converts LanguageExt monads to `ActionResult` or minimal API `IResult`. 

## Quick Reference

- Any monad that has a proper object will return a success code of `200 OK` with a response body
- Any monad that returns `Unit` will return a success code of `204 No Content`
- The `Option<T>` monad will either be a success of `200` or `204` and the none condition is converted to a `404 Not Found`
    - Monad with nested `Option<T>` such as `Fin<Option<T>>` could return `200`, `204`, `404`, or `500` as `Fin<Option<T>>` could be a success with an option of 
      - `Unit` (204)
      - `T` (200)
      - `None` (404)
      - `Error` (500).
- The `Try` monad will return either a 200, 204, or 500
- The `TryOption` monad will return either a 200, 204, 404, or 500
- The `Eff` monad will return a 200, 204, or 500
- The `Aff` monad will return a 200, 204, or 500

Proper IEFT problem detail responses will be presented with the appropriate
status code based on the exception that is contained within the `Fin`, `Try`, `TryOption`, `Eff`, and `Aff` monads. 

## Usage

LanguageExt monads can be converted to Action or IResult. The extensions functions can be used by importing `Oneiro`.


### Quick Start
```csharp
using Oneiro;
//. Other code

IResult result = Try(() => "Hello, World!").ToResult();
```

## Minimal APIs

```csharp
using static LanguageExt.Prelude;
using Oneiro;

interface IService { Option<string> GetMessage(); }

class MyService : IService {
    Option<string> GetMessage() => "Hello, World!";
}

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddTransient<IService, MyService>();

var app = builder.Build();

app.MapGet("/", (IService service) => service.GetMessage().ToResult());

app.Run();
```

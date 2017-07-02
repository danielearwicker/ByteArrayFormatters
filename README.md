# ByteArrayFormatters
Simple mapping between entire HTTP payload and `[FromBody] byte[]` parameter or return value.

## Background

https://stackoverflow.com/questions/44090784/unsupported-media-types-when-post-to-web-api/44823478

## Usage

Install the package to your project:

    Install-Package Earwicker.ByteArrayFormatters

Get access to the namespace:

```csharp
using Earwicker.ByteArrayFormatters;
```

Configure MVC in your `ConfigureServices` method:

```csharp
services.AddMvc(options =>
{
    options.InputFormatters.Add(new ByteArrayInputFormatter());
    options.OutputFormatters.Add(new ByteArrayOutputFormatter());
});
```

You can now use the `[FromBody]` attribute on controller method parameters of type `byte[]`:

```csharp
[HttpPut("files/{*path}")]
public void PutFile(string path, [FromBody] byte[] content)
{
    ...
}
```

You can also return `byte[]` from a controller method. The byte array takes up the entire payload of the HTTP request or response.

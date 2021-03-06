# SodaPop.RazorPagesSitemap

Generates a sitemap based on the layout of your Razor Pages website.

### Status

[![Build status](https://ci.appveyor.com/api/projects/status/vgyismfpwlvny8gq/branch/master?svg=true)](https://ci.appveyor.com/project/Soda-Digital/sodapop-razorpagessitemap/branch/master)

## Install

```
dotnet add package SodaPop.RazorPagesSitemap
```

## Setup

In your `ConfigureServices` method add:

```csharp
services.AddRazorPagesSitemap();
```

In your `Configure` method add (ideally _before_ MVC):
```csharp
app.UseRazorPagesSitemap();
```

## Configuration

You can pass options when configuring the middleware to customize behaviour:

```csharp
services.AddRazorPagesSitemap(options =>
{
    // This will set the <lastmod /> element to be based on the last modified time on disk
    options.BaseLastModOnLastModifiedTimeOnDisk = true; // default is true

    // This will avoid adding duplicate from matching `/mypath` and `/mypath/index`
    options.IgnorePathsEndingInIndex = true; // default is true

    // Allows you to opt out certain patch matches based on regular expressions. In this case
    // we're skipping the pages matching /error/123
    options.IgnoreExpression = @"error\/\d{3}$"; // default is null
});
```

By default, the sitemap will be available at `/sitemap.xml`. You can customize this in your `Configure` method:

```csharp
app.UseRazorPagesSitemap("/myAlternatePath");
```

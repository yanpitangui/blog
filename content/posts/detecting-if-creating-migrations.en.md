---
title: "Detecting if the application is running to create migrations"
date: 2023-06-15T00:52:58-03:00
draft: false
tags: [dotnet, api, ef, migrations]
---

## Problem: Your DbContext has a scoped dependency
Having a scoped dependency, for example in a multi-tenant application, where it injects some scoped service, such as TenantProvider or something like that, you will be unable to create migrations, as the application will not be able to resolve this dependency. But I have the solution!

See the following class as an example:

```csharp
public class Session: ISession {
     public Session(IHttpContextAccessor httpContextAccessor) {...}
}
```

## Solution
One thing you can do is add one more constructor, where you manually add dependencies, like this:
```csharp
public Session(Tenant tenant, Guid userId)
{
     Tenant = tenant;
     UserId = userId;
}
```

Afterwards, use the following code to detect if it is running through EF, that is, there will be no request to capture data in the HttpContext.

```csharp
var isMigration = Assembly.GetEntryAssembly()?.FullName?.StartsWith("ef") ?? false;
```
What this does is basically verify that your application is being called by EfCore.
With this, you can change the behavior of your application, in order to inject a singleton instead of a scoped dependency of your dependency.

Another way to do this, but in my view, more complicated, is using [DesignTimeDbContextFactory](https://learn.microsoft.com/en-us/ef/core/cli/dbcontext-creation?tabs=dotnet-core-cli).

## Full code sample
```csharp
var isMigration = Assembly.GetEntryAssembly()?.FullName?.StartsWith("ef") ?? false;

if (isMigration)
{
     services.AddSingleton<ISession>(_ => new Session(tenantLocal, Session.Admin));
}
else
{
     services.AddScoped<ISession, Session>();
}
```
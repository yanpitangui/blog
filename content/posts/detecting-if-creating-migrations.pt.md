---
title: "Detectando se a aplicação está rodando para criar migrations"
date: 2023-06-15T00:52:58-03:00
draft: false
tags: [dotnet, api, ef, migrations]
---
## Problema: Seu DbContext tem uma dependência scoped
Tendo uma dependência scoped, como por exemplo numa aplicação multi tenant, onde injeta algum serviço scoped, como TenantProvider ou algo do tipo, você ficará impossibilitado(a) de criar migrations, pois a aplicação não conseguirá resolver essa dependência. Mas eu tenho a solução!

Veja a classe a seguir como exemplo: 

```csharp
public class Session: ISession {
    public Session(IHttpContextAccessor httpContextAccessor) {...}
}
```

## Solução
Uma coisa que pode ser feita é adicionar mais um construtor, onde você adiciona manualmente as dependências, como a seguir:
```csharp
public Session(Tenant tenant, Guid userId)
{
    Tenant = tenant;
    UserId = userId;
}
```

Depois, utilize o código a seguir para detectar se está rodando através do EF, ou seja, não existirá request para se capturar dados no HttpContext.

```csharp
var isMigration = Assembly.GetEntryAssembly()?.FullName?.StartsWith("ef") ?? false;
```
O que isso faz é basicamente verificar que a sua aplicação está sendo chamada pelo EfCore.
Com isso, você consegue mudar o comportamento da sua aplicação, afim de injetar um singleton ao invés de uma dependência scoped da sua dependência.

Uma outra maneira de se fazer isso, mas na minha visão, mais complicada, é utilizando [DesignTimeDbContextFactory](https://learn.microsoft.com/en-us/ef/core/cli/dbcontext-creation?tabs=dotnet-core-cli).

## Código completo
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




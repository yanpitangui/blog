---
title: "Deletando chaves do redis por pattern no dotnet"
date: 2023-06-15T15:35:58-03:00
draft: false
tags: [dotnet, redis, key, pattern, delete]
---

## Problema: Você quer deletar mais de uma chave de uma vez, provavelmente por um padrão regex
Utilizando Redis, você deve estar utilizando algo como o seguinte para deletar chaves:
```csharp
public class CacheManager {


    private readonly IDistributedCache _cache;
    public CacheManager(IDistributedCache cache) {
        _cache = cache;
    }

    public async Task RemoveKeys() {
        await Cache.RemoveAsync("chave-1");
        await Cache.RemoveAsync("chave-2");
        await Cache.RemoveAsync("chave-3");
    }
}

``` 
O único problema dessa abordagem é que realizamos um round-trip para cada deleção de chave, ou seja, chamamos o servidor redis a cada deleção.
Em momentos que a latência é importante, e da quantidade de chaves, isso pode fazer uma grande diferença.
E se pudéssemos deletar múltiplas chaves?

## Utilizando regex patterns para deletar múltiplas chaves
A primeira mudança necessária é utilizar um IConnectionMultiplexer, pois precisaremos executar scripts diretamente na instância do redis.
Depois, executar um script Lua, que será o seguinte:

`for i, name in ipairs(redis.call('KEYS', @prefix)) do redis.call('DEL', name); end`

Voltando para o código, ficaríamos com algo como isso: 

```csharp
public class CacheManager
{
    private readonly IDistributedCache _cache; // Talvez você mantenha isso pra utilizar em outros métodos
    private readonly IConnectionMultiplexer _multiplexer;
    public CacheManager(IDistributedCache cache, IConnectionMultiplexer multiplexer)
    {
        _cache = cache;
        _multiplexer = multiplexer;
    }

    public async Task RemoveKeys(string prefix) 
    {
        var prepared = LuaScript.Prepare("for i, name in ipairs(redis.call('KEYS', @prefix)) do redis.call('DEL', name); end");
        await _multiplexer.GetDatabase().ScriptEvaluateAsync(prepared, new { prefix = prefix });
    }

}

// Aí, utilizamos assim:
... 
await manager.RemoveKeys("chave-*");

```



## Links relevantes
- https://stackexchange.github.io/StackExchange.Redis/Scripting
- https://stackoverflow.com/a/27561399/12881014



---
title: "Deleting Redis keys by pattern in dotnet"
date: 2023-06-15T15:35:58-03:00
draft: false
tags: [dotnet, redis, key, pattern, delete]
---

## Problem: You want to delete more than one key at a time, probably by regex pattern
Using Redis, you might be using something like the following to delete keys:
```csharp
public class CacheManager {


     private readonly IDistributedCache _cache;
     public CacheManager(IDDistributedCache cache) {
         _cache = cache;
     }

     public async Task RemoveKeys() {
         await Cache.RemoveAsync("key-1");
         await Cache.RemoveAsync("key-2");
         await Cache.RemoveAsync("key-3");
     }
}

```
The only problem with this approach is that we perform a round-trip for each key deletion, that is, we call the redis server at each deletion.
In times when latency is important, and the number of keys, this can make a big difference.
What if we could delete multiple keys?

## Using regex patterns to delete multiple keys
The first necessary change is to use an IConnectionMultiplexer, as we will need to run scripts directly on the redis instance.
Afterwards, execute a Lua script, which will be the following:

`for i, name in ipairs(redis.call('KEYS', @prefix)) do redis.call('DEL', name); end`

Going back to the code, we would end up with something like this:

```csharp
public class CacheManager
{
     private readonly IDistributedCache _cache; // Maybe you can keep this for use in other methods
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

// Then, we use it like this:
...
await manager.RemoveKeys("key-*");

```



## Relevant links
- https://stackexchange.github.io/StackExchange.Redis/Scripting
- https://stackoverflow.com/a/27561399/12881014
---
tags:
	- web-development
	- caching
	- redis
category: Web Development
related: REST API, Server-Side vs Client-side operations, File IO
---

# Cache and Redis

A cache stores data temporarily so future requests can be served faster and with less work. Redis is an in-memory data store commonly used as a distributed cache, session store, message broker, and fast key-value database.

## Why Use a Cache?

Caching can reduce database load, lower latency, and improve resilience during traffic spikes. The tradeoff is that cached data may become stale and adds another system to operate.

```text
Request -> Check cache -> Hit: return cached value
										-> Miss: read source -> store result -> return value
```

## Cache-Aside Pattern

The application manages the cache explicitly:

```csharp
var cacheKey = $"product:{productId}";
var product = await cache.GetStringAsync(cacheKey);

if (product is null)
{
		product = await database.GetProductAsync(productId);
		await cache.SetStringAsync(
				cacheKey,
				Serialize(product),
				new DistributedCacheEntryOptions
				{
						AbsoluteExpirationRelativeToNow = TimeSpan.FromMinutes(10)
				});
}

return product;
```

The application reads from Redis first, loads the source of truth on a miss, and writes the result back with an expiration time.

## Redis Data Types

| Type | Useful for |
|------|------------|
| String | Values, JSON documents, counters, tokens |
| Hash | Fields belonging to one object |
| List | Queues and ordered items |
| Set | Unique values and membership checks |
| Sorted set | Rankings and time-based ordering |
| Stream | Append-only event processing |

## Expiration and Invalidation

Every cached value should have a deliberate expiration policy unless it is explicitly permanent. Common strategies include:

- **TTL expiration** - Remove data after a fixed period.
- **Write invalidation** - Delete or update the key when the source changes.
- **Versioned keys** - Change the key when the data shape or version changes.
- **Stale-while-revalidate** - Serve an older value while refreshing it in the background.

Invalidation is often harder than reading from a cache. Define what happens when an update, delete, failed refresh, or partial outage occurs.

## Redis Considerations

- Use namespaced, predictable keys such as `catalog:product:42`.
- Keep values small and serialize them consistently.
- Set timeouts so a cache outage does not block every request.
- Avoid caching sensitive data without encryption and access controls.
- Prevent cache stampedes with locking, jittered expiration, or request coalescing.
- Monitor hit rate, memory usage, evictions, latency, and connection errors.

## When Not to Cache

Do not cache data when freshness is more important than latency, the source is already fast, values are highly unique, or invalidation cannot be made safe. Caching a slow or incorrect design without measuring it can hide the real problem.

## Related Concepts

- [[REST API]] - APIs often use caching for repeated reads
- [[Server-Side vs Client-side operations]] - Decide where caching belongs
- [[File IO]] - Another form of data persistence
- [[Error Handling]] - Handle cache failures and fallbacks

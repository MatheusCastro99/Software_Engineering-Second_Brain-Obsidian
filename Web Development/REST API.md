---
tags:
	- web-development
	- api
	- http
category: Web Development
related: Server-Side vs Client-side operations, Cache and Redis, Error Handling
---

# REST API

A REST API exposes resources over HTTP using predictable URLs, methods, representations, and status codes. REST is an architectural style, not a single library or protocol separate from HTTP.

## Resources and URLs

Use nouns to identify resources and HTTP methods to express the operation:

| Method | Example | Purpose |
|--------|---------|---------|
| GET | `/api/products/42` | Read a resource |
| POST | `/api/products` | Create a resource or trigger a subordinate action |
| PUT | `/api/products/42` | Replace a resource |
| PATCH | `/api/products/42` | Partially update a resource |
| DELETE | `/api/products/42` | Remove a resource |

```text
GET /api/products?category=hardware&page=2&pageSize=20
```

Query parameters are useful for filtering, sorting, searching, and pagination. Keep resource identifiers stable and avoid exposing database implementation details unnecessarily.

## HTTP Status Codes

| Status | Meaning | Typical use |
|--------|---------|-------------|
| 200 OK | Request succeeded | Successful read or update |
| 201 Created | Resource created | Successful POST, usually with a `Location` header |
| 204 No Content | Succeeded without a body | Successful delete |
| 400 Bad Request | Invalid request syntax or data | Malformed input |
| 401 Unauthorized | Authentication required or failed | Missing or invalid identity |
| 403 Forbidden | Authenticated but not allowed | Authorization failure |
| 404 Not Found | Resource does not exist | Unknown identifier |
| 409 Conflict | State conflict | Duplicate or concurrent update |
| 500 Internal Server Error | Unexpected server failure | Unhandled backend error |

## Request and Response Design

```json
{
	"id": 42,
	"name": "Keyboard",
	"price": 49.99,
	"links": {
		"self": "/api/products/42"
	}
}
```

Use consistent field names, predictable error shapes, and explicit date and number formats. Never return stack traces, secrets, or internal database errors to clients.

## Statelessness and Idempotency

Each request should contain the information needed to process it; the server should not depend on hidden client session state for ordinary resource operations. `GET`, `PUT`, and `DELETE` are intended to be idempotent: repeating the same request produces the same intended result, even if the response differs.

For operations where clients may retry, use idempotency keys or a request identifier so a network retry does not create duplicate work.

## Authentication and Authorization

Authentication answers who the caller is. Authorization answers what that caller may do. Enforce authorization on the server for every protected resource and action. Do not rely on a hidden UI control or client-provided role.

## API Quality Practices

- Validate all input at the boundary.
- Support pagination for potentially large collections.
- Version or evolve contracts deliberately.
- Apply rate limits and request-size limits.
- Log correlation IDs without logging credentials or sensitive payloads.
- Document endpoints with an OpenAPI specification when appropriate.
- Test success, validation, authorization, not-found, and failure paths.

## Related Concepts

- [[Server-Side vs Client-side operations]] - API responsibility boundaries
- [[Cache and Redis]] - Cache safe, repeated API reads
- [[Error Handling]] - Consistent failure responses
- [[Popular Stacks and Frameworks]] - Frameworks for implementing APIs

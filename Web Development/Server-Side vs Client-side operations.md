---
tags:
	- web-development
	- architecture
	- client-server
category: Web Development
related: REST API, DOM, Cache and Redis, Popular Stacks and Frameworks
---

# Server-Side vs Client-Side Operations

Web applications divide work between the server and the client. The server runs in a controlled environment and owns protected data and business rules. The client runs in the user's browser or application and manages presentation and interaction.

## Server-Side Operations

The server commonly handles:

- Authentication and authorization
- Business rules and validation
- Database access and transactions
- Rendering or preparing application data
- Calling protected external services
- Logging, rate limiting, and security controls

Server-side code must treat all client input as untrusted. A browser can be modified, bypassed, or replaced by a direct HTTP client.

## Client-Side Operations

The client commonly handles:

- Rendering the interface
- Capturing input and responding to events
- Immediate validation and feedback
- Managing local UI state
- Calling APIs and displaying results
- Accessibility and browser-specific interaction

Client-side validation improves user experience but does not replace server-side validation.

## Request Lifecycle

```text
Browser event
		-> Client-side validation
		-> HTTP request
		-> Server authentication and validation
		-> Business logic and data access
		-> HTTP response
		-> Client updates the DOM
```

The client should receive only the data it needs. The server should return a clear status code and response shape so the client can handle success and failure consistently.

## Rendering Strategies

| Strategy | Where HTML is produced | Strength |
|----------|-------------------------|----------|
| Server-side rendering | Server | Fast initial content and strong control |
| Client-side rendering | Browser | Rich interactions after the app loads |
| Static generation | Build process | Fast, cacheable content |
| Hybrid rendering | Multiple locations | Balance initial load and interactivity |

The right strategy depends on SEO, interactivity, device constraints, data freshness, and operational complexity.

## What Belongs Where?

| Concern | Preferred owner |
|---------|-----------------|
| Password verification | Server |
| Database query | Server |
| Button enabled state | Client |
| Final authorization decision | Server |
| Immediate format hint | Client, then server validation |
| Secret API key | Server |
| Accessible focus management | Client |
| Cache policy | Shared decision; enforce protected rules server-side |

## Security Boundary

The server is the security boundary. Never trust hidden form fields, disabled buttons, client-side role checks, or values stored in browser storage for authorization. Use HTTPS, secure cookie settings, input validation, output encoding, and appropriate anti-forgery protections.

## Performance Tradeoffs

Moving work to the client can reduce server computation but increases JavaScript size, device CPU usage, and exposure of implementation details. Moving work to the server can improve control and initial delivery but may increase request latency and server load. Measure the real workflow instead of assuming one side is always faster.

## Related Concepts

- [[REST API]] - The communication boundary between client and server
- [[DOM]] - Client-side document updates
- [[Cache and Redis]] - Caching at different layers
- [[Popular Stacks and Frameworks]] - Technologies that implement each side
- [[Error Handling]] - Handle failures across the boundary

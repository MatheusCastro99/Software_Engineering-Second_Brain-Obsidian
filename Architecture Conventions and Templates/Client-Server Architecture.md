---
tags:
  - architecture
  - networking
  - web-development
category: Architecture Conventions and Templates
related: Server-Side vs Client-side operations, REST API, MVC, Full Stack, Front End, and Back End Development
---

# Client-Server Architecture

Client-server architecture splits a system into **clients**, which request resources or services, and **servers**, which provide them. Clients and servers communicate over a network using an agreed protocol such as HTTP. Most modern software follows this model: browsers and mobile apps are clients; web APIs, databases, and file servers are servers.

## Core Idea

```text
┌──────────┐    request (HTTP, TCP)    ┌──────────┐
│  Client  │ ────────────────────────► │  Server  │
│ browser, │                           │ API, DB, │
│ app, CLI │ ◄──────────────────────── │  files   │
└──────────┘         response          └──────────┘
```

- The **client** starts the communication, displays results, and handles user interaction.
- The **server** listens for requests, applies business rules, accesses data, and returns responses.
- One server usually serves **many** clients at the same time.

## Tiers

| Model | Layout | Example |
|-------|--------|---------|
| **2-tier** | Client ↔ Database | Desktop app querying SQL Server directly |
| **3-tier** | Client ↔ Application server ↔ Database | Browser → ASP.NET Core API → SQL database |
| **N-tier** | Adds caches, queues, gateways, and more services | Browser → CDN → API gateway → services → Redis/DB |

The 3-tier model is the most common for web apps: the client never talks to the database directly, which protects data and centralizes rules.

## Example: C# Client Calling a Server

```csharp
// Server (ASP.NET Core minimal API)
var app = WebApplication.Create(args);
app.MapGet("/api/products/{id}", (int id) => new { Id = id, Name = "Keyboard" });
app.Run();
```

```csharp
// Client (console app)
using var http = new HttpClient { BaseAddress = new Uri("https://localhost:5001") };
var product = await http.GetFromJsonAsync<Product>("/api/products/1");
Console.WriteLine(product?.Name);

public record Product(int Id, string Name);
```

The client and server only share the **contract**: the URL, HTTP method, and JSON shape (see [[REST API]] and [[Serializations]]).

## Thin vs Thick Clients

| Type | Where logic runs | Example |
|------|------------------|---------|
| **Thin client** | Mostly on the server | Server-rendered web pages |
| **Thick (rich) client** | Much on the client | SPA (React, Blazor WebAssembly), desktop apps |

Rules that protect data, like validation, authorization, and pricing, must always be enforced on the server, even if the client also checks them. See [[Server-Side vs Client-side operations]].

## Client-Server vs Peer-to-Peer

| Aspect | Client-Server | Peer-to-Peer |
|--------|---------------|--------------|
| Roles | Fixed (client or server) | Every node can be both |
| Control | Centralized | Distributed |
| Examples | Web apps, email, databases | File sharing, some multiplayer games |

## Advantages and Trade-offs

**Advantages**
- Centralized data, security, and updates
- Clients can be simple and platform-independent
- Servers can scale (more instances, load balancers, caching)

**Trade-offs**
- The server is a single point of failure unless made redundant
- Network latency and availability affect every interaction
- Heavy load needs scaling strategies (see [[Cache and Redis]], [[Kubernetes]])

## Related Concepts

- [[Server-Side vs Client-side operations]] - Deciding where each responsibility runs
- [[REST API]] - The most common client-server contract on the web
- [[Full Stack, Front End, and Back End Development]] - Front end = client, back end = server
- [[MVC]] - A common pattern on the server side
- [[Microservices Architecture]] - Splits the server side into many services
- [[Monolith - Modular Monolith]] - A single server-side application

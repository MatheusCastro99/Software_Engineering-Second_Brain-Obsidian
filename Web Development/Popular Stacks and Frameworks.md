---
tags:
	- web-development
	- frameworks
	- architecture
category: Web Development
related: Server-Side vs Client-side operations, REST API, DOM
---

# Popular Stacks and Frameworks

A web stack is the collection of technologies used to build, run, and deliver a web application. A framework supplies conventions and reusable infrastructure for common concerns such as routing, rendering, data access, validation, and testing.

## Stack Layers

| Layer | Responsibility | Examples |
|-------|----------------|----------|
| Browser | Render UI and handle interaction | HTML, CSS, JavaScript |
| Client framework | Organize interactive components | React, Angular, Vue |
| Server runtime | Execute backend code | .NET, Node.js, Java, Python |
| Web framework | Routing, middleware, rendering, APIs | ASP.NET Core, Express, Django, Spring |
| Data layer | Store and retrieve data | SQL databases, MongoDB, Redis |
| Delivery | Build, host, and observe the application | Docker, cloud platforms, CI/CD |

## Common Stack Families

### .NET Stack

ASP.NET Core provides routing, middleware, dependency injection, authentication integration, and REST API support. It pairs naturally with C#, Entity Framework Core, SQL databases, and client frameworks such as React or Blazor.

### JavaScript and TypeScript Stack

Node.js runs JavaScript outside the browser. Express and similar frameworks provide lightweight server routing, while TypeScript adds static type checking. React, Vue, and Angular are commonly used for client applications.

### Python Stack

Django provides a batteries-included framework with routing, models, administration, and security features. Flask and FastAPI are smaller alternatives often used for focused services and APIs.

### Java Stack

Spring Boot provides a large ecosystem for APIs, web applications, security, data access, and enterprise integration.

## Monolith, Modular Monolith, and Services

- **Monolith** - One deployable application containing multiple features.
- **Modular monolith** - One deployment with strong internal boundaries.
- **Distributed services** - Multiple independently deployed applications communicating over APIs or messaging.

Start with the simplest architecture that satisfies the requirements. Splitting a system into services adds deployment, networking, observability, and data-consistency costs.

## Choosing a Framework

Evaluate a framework by:

- Team familiarity and hiring availability
- Documentation and long-term maintenance
- Security defaults and upgrade process
- Testing and debugging support
- Performance requirements and hosting options
- Integration with databases, identity, and deployment systems
- Accessibility and client-side rendering needs

Framework popularity is not enough. A smaller, well-supported framework that fits the team can be a better choice than a fashionable tool with a poor operational fit.

## Best Practices

- Keep business rules independent from framework-specific code where practical.
- Follow the framework's conventions before adding custom abstractions.
- Pin and regularly update dependencies.
- Define API and data boundaries explicitly.
- Measure performance with realistic workloads.
- Document the reasons behind major stack decisions.

## Related Concepts

- [[Server-Side vs Client-side operations]] - Place responsibilities across the stack
- [[REST API]] - Communication between applications
- [[DOM]] - Browser document manipulation
- [[Cache and Redis]] - Improve data access performance
- [[Docker Basics]] - Package and deploy applications

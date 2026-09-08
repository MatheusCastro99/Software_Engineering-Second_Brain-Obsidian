---
tags:
	- web-development
	- full-stack
	- architecture
category: Web Development
related: DOM, REST API, Server-Side vs Client-side operations, Popular Stacks and Frameworks
---

# Full-Stack, Front-End, and Back-End Development

Web applications are commonly described in three connected areas. **Front-end development** builds the interface that runs in the browser. **Back-end development** implements server-side behavior, data access, and business rules. **Full-stack development** works across both sides and the boundaries between them.

## Front-End Development

Front-end code commonly handles:

- Rendering pages and components
- User interaction and browser events
- Client-side state and navigation
- Immediate validation and feedback
- Accessibility and responsive layout
- Calling APIs and presenting results

The browser is an untrusted environment. Client-side checks improve usability but cannot enforce authorization or protect secrets.

## Back-End Development

Back-end code commonly handles:

- Authentication and authorization
- Business rules and server-side validation
- API endpoints and integration with other services
- Database queries and transactions
- Background processing and scheduled work
- Logging, monitoring, and security controls

The back end is responsible for enforcing the rules that must remain true regardless of which client sends a request.

## Full-Stack Development

Full-stack development requires understanding the complete request path:

```text
Browser UI -> HTTP request -> API and business logic -> Database or service
Browser UI <- HTTP response <- API and business logic <- Database or service
```

A full-stack developer does not need to be an expert in every technology. The essential skill is reasoning about contracts, data flow, failure modes, security boundaries, and deployment across the system.

## Boundaries and Contracts

The front end and back end communicate through an explicit contract, usually an API. The contract should define request fields, response shapes, status codes, validation errors, authentication behavior, and versioning expectations.

```json
{
	"error": {
		"code": "VALIDATION_ERROR",
		"message": "Email is required",
		"field": "email"
	}
}
```

Consistent contracts reduce duplicated assumptions and make independent development easier.

## Common Architectures

| Architecture | Description |
|--------------|-------------|
| Server-rendered | Server produces HTML and the browser enhances or submits it |
| Single-page application | Browser loads an application and communicates with APIs |
| Static site with APIs | Prebuilt pages use APIs for dynamic operations |
| Full-stack framework | One framework coordinates server and client rendering |

Choose based on interactivity, SEO, performance, team skills, hosting, accessibility, and data requirements.

## Shared Concerns

Some concerns cross the front-end and back-end boundary:

- Identity and authorization
- Validation and error handling
- Serialization and date formats
- Caching and performance
- Observability and correlation IDs
- Testing and deployment

## Best Practices

- Keep business rules on the server even when the UI also validates them.
- Define API contracts before implementing both sides.
- Avoid exposing database models directly when a separate API model is clearer.
- Use consistent loading, empty, success, and error states in the UI.
- Test the boundary with integration and contract tests.
- Document environment variables and deployment assumptions.

## Related Concepts

- [[DOM]] - Browser document and interaction model
- [[REST API]] - Communication between application layers
- [[Server-Side vs Client-side operations]] - Responsibility boundaries
- [[Popular Stacks and Frameworks]] - Technologies used across the stack
- [[Serializations]] - Represent data across boundaries

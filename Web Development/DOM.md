---
tags:
  - web-development
  - javascript
  - dom
category: Web Development
related: Server-Side vs Client-side operations, REST API, Error Handling
---

# Document Object Model (DOM)

The Document Object Model (DOM) is the browser's object representation of an HTML document. It organizes the page as a tree of nodes that client-side code can read, change, and respond to.

## DOM Tree

```text
document
└── html
	├── head
	└── body
		├── header
		└── main
			└── button
```

Elements, attributes, text, and events are exposed through objects and properties. JavaScript uses the global `document` object to access the tree.

## Selecting Elements

```javascript
const title = document.querySelector('h1');
const saveButton = document.querySelector('#save-button');
const rows = document.querySelectorAll('.result-row');

title.textContent = 'Results';
saveButton.disabled = true;
```

Prefer specific selectors and stable IDs or classes. A selector that depends on fragile layout details can break when the HTML changes.

## Creating and Updating Content

```javascript
const message = document.createElement('p');
message.className = 'status-message';
message.textContent = 'Saved successfully';
document.querySelector('#status').append(message);
```

Use `textContent` for untrusted text. Assigning untrusted input to `innerHTML` can create a cross-site scripting vulnerability unless the content is safely sanitized.

## Events

Events represent user or browser activity such as clicks, input, submission, and page loading.

```javascript
const form = document.querySelector('#search-form');

form.addEventListener('submit', async (event) => {
	event.preventDefault();
	const query = new FormData(form).get('query');
	await searchProducts(query);
});
```

### Event Bubbling and Delegation

Most events bubble from the target toward its ancestors. Event delegation attaches one handler to a stable parent, which is useful for lists whose children are created dynamically.

```javascript
document.querySelector('#results').addEventListener('click', (event) => {
	const row = event.target.closest('[data-product-id]');
	if (row) openProduct(row.dataset.productId);
});
```

## Performance and Accessibility

- Batch DOM changes instead of repeatedly forcing layout calculations.
- Avoid unnecessary full-page re-rendering for small updates.
- Use semantic HTML before adding ARIA attributes.
- Keep keyboard focus visible and move focus deliberately after dynamic changes.
- Clean up event listeners when components are removed.
- Test behavior with keyboard navigation and assistive technology.

## DOM vs. Virtual DOM

The browser DOM is the actual document interface. Some UI libraries maintain a virtual representation and calculate a smaller set of DOM updates. This can simplify component rendering, but it does not remove the need to understand browser events, layout, accessibility, and performance.

## Related Concepts

- [[Server-Side vs Client-side operations]] - Where browser code runs
- [[REST API]] - Retrieve or submit data from the browser
- [[Error Handling]] - Handle failed client-side operations
- [[Popular Stacks and Frameworks]] - Libraries that manage UI updates

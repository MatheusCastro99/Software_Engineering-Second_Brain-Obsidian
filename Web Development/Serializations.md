---
tags:
	- web-development
	- data
	- serialization
category: Web Development
related: REST API, File IO, Server-Side vs Client-side operations
---

# Serialization

Serialization is the process of converting an in-memory object or data structure into a format that can be stored or transmitted. Deserialization reconstructs usable data from that representation.

```text
Object -> Serialize -> Text or bytes -> Transfer or storage
Object <- Deserialize <- Text or bytes <- Transfer or storage
```

Serialization is used in APIs, files, caches, messaging systems, databases, and distributed applications. The serialized format becomes a contract, so changes must be made deliberately.

## JSON

JSON is a lightweight, text-based format commonly used by web APIs. It represents objects, arrays, strings, numbers, booleans, and null values.

```json
{
	"id": 42,
	"name": "Keyboard",
	"tags": ["hardware", "input"]
}
```

Advantages include broad language support, readability, and simple browser integration. JSON does not preserve every programming-language type, so dates, decimals, enums, and polymorphic objects need an agreed representation.

## XML

XML is a text-based, hierarchical format that uses elements and attributes.

```xml
<product id="42">
	<name>Keyboard</name>
	<category>hardware</category>
</product>
```

XML supports namespaces, schemas, mixed content, and mature document-processing tools. It can be more verbose than JSON but remains common in enterprise integrations, configuration, and standards-based systems.

## Binary Serialization

Binary serialization represents data as bytes rather than human-readable text. Formats include protocol buffers, MessagePack, Avro, and custom binary protocols.

Binary formats can reduce size and improve parsing speed, but they are harder to inspect manually and may require a shared schema or compatible library. Never deserialize untrusted binary data using a mechanism that can execute arbitrary types or code.

## Format Comparison

| Format | Strengths | Tradeoffs | Common use |
|--------|-----------|-----------|------------|
| JSON | Readable, widely supported | Larger payloads, limited type system | REST APIs and browser data |
| XML | Schemas, namespaces, mature tooling | Verbose and complex | Enterprise and document integration |
| Binary | Compact and efficient | Less readable, schema concerns | Services, messaging, storage |

## Versioning and Compatibility

Serialized data can outlive the code that created it. Prefer additive changes when possible, provide defaults for new fields, tolerate unknown fields when safe, and document breaking changes. Test old data against new readers and new data against supported readers.

## Security and Reliability

- Validate size, structure, types, and allowed values before deserialization.
- Treat all external data as untrusted input.
- Avoid insecure object deserialization.
- Protect sensitive fields during storage and transmission.
- Define encoding, date, time-zone, and numeric conventions.
- Handle malformed, truncated, and version-incompatible data explicitly.

## Related Concepts

- [[REST API]] - Serialization at an HTTP boundary
- [[File IO]] - Serialize data to and from files
- [[Server-Side vs Client-side operations]] - Exchange data between application layers
- [[Cache and Redis]] - Store serialized values in a cache
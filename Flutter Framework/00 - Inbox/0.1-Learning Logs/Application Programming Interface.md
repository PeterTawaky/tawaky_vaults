---
tags:
  - api
type: Linking Note
connections:
  - "[[HTTP Protocol Methods]]"
aliases:
  - API
---
### What is API?
- set of rules and protocols that allows different software applications to communicate with each other.
- Links between client and data base

### API paradigms:
	What API made from, this part belongs to the Backend Engineer.

| Paradigm      | Protocol  | Use Case Example       | Data Format | Best For                     | Example Use Case        |
| ------------- | --------- | ---------------------- | ----------- | ---------------------------- | ----------------------- |
| **REST**      | HTTP      | CRUD APIs, mobile apps | JSON/XML    | Simple, stateless            | Twitter API             |
| **GraphQL**   | HTTP      | Custom data fetching   | JSON        | Efficient, client-controlled | GitHub API v4           |
| **WebSocket** | WS        | Real-time apps         | JSON/Binary | Live updates, bidirectional  | Chat apps               |
| **SOAP**      | HTTP/SMTP | Enterprise/finance     | XML         | Secure, standardized         | Bank transactions       |
| **gRPC**      | HTTP/2    | Microservices          | Protobuf    | Fast, contract-first         | Cloud services (Google) |
| **Webhook**   | HTTP      |                        | JSON/XML    | Event notifications          | Stripe payment alerts   |
___
- `baseUrl` variable for all methods : Domain + Path
JSON: java script object notation
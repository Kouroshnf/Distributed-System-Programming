# Lab 01 — Film Manager REST API

**Distributed Systems Programming · A.Y. 2026/2027 · Politecnico di Torino**

**Status:** In progress

## Overview

Lab 01 focuses on the **design of JSON Schemas** and the **design and implementation of REST APIs** using a *Film Manager* application. Film Manager enables users to record films, distinguish public and private entries, and invite other users to review public films.

The objective is to model resources correctly, describe their HTTP interfaces in OpenAPI, and connect the API to an existing service implementation through generated routing adapters and handwritten controllers.

## Learning objectives

- Model users, films, and review invitations using **JSON Schema Draft 7**.
- Validate example JSON documents against those schemas.
- Define resources, HTTP operations, parameters, request/response bodies, status codes, and security in **OpenAPI**.
- Generate a server routing stub from the API specification.
- Implement controller logic for request validation, service invocation, HTTP responses, and **HATEOAS** links.
- Test public and authenticated operations using an HTTP client.

## Application model

| Resource | Main properties and constraints |
| --- | --- |
| **User** | `id` (required), `name`, `email` (required; valid email), `password` (6–20 characters if present). |
| **Film** | `id`, `title`, `owner`, and `private` are required. `watchDate` (`YYYY-MM-DD`), `rating` (integer 0–10), and `favorite` (default `false`) are allowed only for private films. |
| **Review invitation / review** | `filmId`, `reviewerId`, and `completed` are required. When `completed` is `true`, `reviewDate` (`YYYY-MM-DD`), `rating` (integer 0–10), and `review` (maximum 1,000 characters) are required; when false, these fields must not be included. |

These constraints summarize the assignment; the actual schemas must enforce them.

## Functional requirements

### Public access

Unauthenticated clients may log in, access the Film Manager entry point, list or retrieve public films, and list or retrieve reviews associated with public films.

### Authenticated access

- Create films; the creator becomes the owner.
- Read public films or private films owned by the current user.
- List owned films and films assigned to the user for review.
- Update or delete owned films; a film's public/private visibility cannot be changed by an update.
- Invite one or more users (including the owner) to review a **public** film.
- Remove an invitation only while the review is incomplete.
- Complete an assigned review by supplying its date, rating, and text.

The API must also **design** an operation that distributes invitations approximately evenly among users for films without invitations. **Implementation of this distribution operation is not required.** Pagination of film lists is recommended.

## Technologies and prerequisites

| Tool | Purpose |
| --- | --- |
| VS Code | Editing and JSON validation |
| OpenAPI (Swagger) Editor | Authoring the API specification |
| Node.js **22** and npm | JavaScript runtime and dependencies |
| Express | HTTP server framework |
| Java and OpenAPI Generator | Server-stub generation |
| Postman | Testing requests and responses |
| SQLite / DB Browser for SQLite | Inspecting the provided database |

The supplied project additionally uses **AJV** for validation, **Passport** and **express-session** for cookie-based sessions, and **bcrypt** for password hashing.

## Starter project and organization

**Important:** For the API implementation, use the course-provided project rather than creating a new Express application from scratch:

[Official Lab 01 starter repository](https://github.com/polito-DSP-2026-2027/lab01)

According to the lab presentation, the starter skeleton is scheduled to become available **October 19, 2026**. Access may depend on course enrollment or permissions.

The instructor's project is expected to include the following key locations:

```text
Lab01/
├── README.md                 # This laboratory overview
├── package.json              # Dependencies and project scripts
├── index.js                  # Express server setup
├── passport-config.js        # Authentication configuration
├── api/
│   └── openapi.json          # OpenAPI specification — to complete
├── json-schemas/             # Draft 7 schemas — to complete
├── controllers/              # REST controllers — to complete
│   ├── validator.js          # Provided AJV configuration
│   └── link.js               # HATEOAS helpers — to complete
├── service/                  # Provided application/business logic
├── database/                 # Provided SQLite data
├── components/               # Resource definitions
├── utils/                    # Supporting utilities
├── openapi-templates/        # Generator templates
├── openapitools.json         # Generator configuration
└── generated/                # Auto-generated routing adapters
```

This is the **expected structure after incorporating the official starter**, not a claim that all files already exist locally. Preserve the instructor's actual file organization and its original README/setup guidance when importing it.

## Implementation plan

- [ ] **Part 1 — JSON schemas:** Create Draft 7 schemas for users, films, and reviews in `json-schemas/`.
- [ ] **Part 1 — Validation:** Create valid and invalid sample JSON documents; check error messages in VS Code's **Problems** view (`Ctrl+Shift+M`).
- [ ] **Part 2 — OpenAPI:** Complete `api/openapi.json` with endpoints, tags, `operationId`s, parameters, input/output schemas, status codes, and `cookieAuth` where required.
- [ ] **Part 2 — Generation:** Run `npm run generate` from the supplied project's root to create/update the routing adapters.
- [ ] **Part 2 — HATEOAS:** Replace `/change/me` placeholders and complete link helpers in `controllers/link.js`.
- [ ] **Part 2 — Controllers:** Implement request/parameter validation, calls into the provided service layer, HTTP responses, and resource links.
- [ ] **Part 2 — Testing:** Verify public endpoints, authorization boundaries, CRUD operations, reviews, and invalid-input responses in Postman.
- [ ] **Part 2 — Design-only operation:** Specify automatic fair distribution of review invitations; implementation is optional/not required.

### Generated routing and controller mapping

The OpenAPI specification determines dispatch:

- The **first operation tag** identifies the corresponding controller file.
- The **`operationId`** identifies the function exported by that controller.
- The generator creates routing adapters under `generated/`.

Do **not** manually edit generated adapters: rerun `npm run generate` after changing the OpenAPI specification.

### Controller responsibilities

Controllers should validate JSON input with the provided AJV validators, verify parameters, invoke appropriate `service/` functions, translate results into HTTP status codes and response bodies, and add HATEOAS links via the provided link helpers.

## Local setup and testing

After the official starter project has been added:

```bash
cd Lab01
npm install
npm run generate
```

Check the supplied `package.json` and the official starter README for the **correct command to start the server**. It is not specified in the two course PDFs. Use Postman to test the server's documented base URL and endpoints once it is running.

Authentication is **session-based**, using a server-side session and a cookie. The course uses HTTP for local debugging; that configuration is **not suitable for production deployment**, where HTTPS is needed.

## Notes and good practices

- Store hashed—not plaintext—passwords; the specification requires a random salt of at least 16 bytes.
- Do not publish credentials from the provided database or any secret/configuration files.
- Keep the supplied service-layer code separate from REST-specific controller responsibilities.
- Keep documentation and test examples updated as endpoint behavior changes.
- Follow any course rules about sharing provided materials and assignment solutions.

## References

- *Distributed Systems Programming — Laboratory 1*, A.Y. 2026/27 (course handout)
- *Laboratory Activity #01* (course presentation)
- [Course starter repository](https://github.com/polito-DSP-2026-2027/lab01)
- [JSON Schema Draft 7](https://json-schema.org/draft-07/schema)
- [OpenAPI Specification](https://swagger.io/specification/)

---

*This README tracks the intended assignment and progress; completing the checklist and confirming setup commands is part of the lab work.*

For validation and testing use this command : 
- npx ajv-cli validate -s json-schemas/Users.json -d json-schemas-test/UserTest.json

in simple we can change the name of Users.json and UserTest.json with a valid name that we want to check.

# Distributed-System-Programming
Laboratory exercises and projects for the Distributed Systems Programming university course.

**Politecnico di Torino · Academic Year 2026/2027**

A collection of laboratory exercises and implementations developed for the **Distributed Systems Programming** course. Each laboratory is organized in its own directory, with source code, relevant configurations, testing material, and a README documenting its goals and results.

## Repository overview

The repository tracks practical work on distributed applications and their interfaces. It is intended as a structured record of the design decisions, implementations, and tests carried out throughout the course—not as a single monolithic application.

## Laboratories

| Laboratory | Project | Main topics | Progress |
| --- | --- | --- | --- |
| [Lab 01](./Lab01/) | Film Manager | JSON Schema Draft 7, REST API design, OpenAPI, Node.js/Express, API testing | In progress |

Additional labs will be added as their assignments become available.

## Repository structure

```text
Distributed-System-Programming/
├── README.md             # Course overview and laboratory index
└── Lab01/
    ├── README.md         # Lab 01 objectives, tasks, and instructions
    └── ...               # Lab 01 source files and course starter project
```

The exact contents of each lab directory follow its assignment and, where provided, the instructor's starter project.

## Development approach

For each laboratory:

1. Read the assignment and identify the required deliverables.
2. Set up the recommended tools and the provided starter project, if any.
3. Implement the tasks incrementally, keeping changes within that lab's directory.
4. Validate inputs, run the application where applicable, and test the required behavior.
5. Document design decisions, how to reproduce the work, and any remaining limitations.
6. Commit completed milestones with descriptive Git messages.

## Tools and technologies

The stack varies by lab. **Lab 01** uses or recommends:

- **Visual Studio Code** and the **OpenAPI (Swagger) Editor** extension
- **JSON Schema Draft 7** and **OpenAPI**
- **JavaScript**, **Node.js 22**, **npm**, and **Express**
- **Java** and **OpenAPI Generator** for generating server-side routing code
- **Postman** for HTTP API testing
- **SQLite** and **DB Browser for SQLite** for database inspection

These are Lab 01 requirements and recommendations, not necessarily requirements for every future laboratory.

## Getting started

Clone the repository and open it in VS Code:

```bash
git clone https://github.com/Kouroshnf/Distributed-System-Programming.git
cd Distributed-System-Programming
code .
```

Then navigate to the relevant lab directory and follow its README. Setup and execution steps differ between laboratories.

## Academic context and attribution

The laboratory specifications and starter material are supplied by the **Distributed Systems Programming** teaching team at **Politecnico di Torino**. This repository is a personal coursework workspace and is not an official course repository. Where instructor-provided files are included, their origin should remain clear.


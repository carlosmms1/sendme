---
id: 0003
title: ORM Selection GORM
status: accepted
date: 2025-05-15
---

# ORM Selection GORM

## Context and Problem Statement

The project requires persistent storage of URL mappings and related metadata. Using an ORM can significantly simplify data modeling, migrations, and database interactions.

## Considered Options

- **GORM:** A widely adopted ORM in the Go community. It provides abstractions for database interactions, automates migrations, and offers rich querying capabilities.
- **sqlc:** A tool that generates type-safe Go code from raw SQL queries. It provides maximum performance and control but demands detailed knowledge of SQL and generates more boilerplate.

## Decision Outcome

We decided to use **GORM** as the ORM for the MVP of this project.

## Consequences

- Possible performance trade-offs in high-load scenarios.
- Future migration to `sqlc` or raw SQL may be considered if performance becomes critical.
- We gain speed and flexibility for the MVP while maintaining a clear path for future optimization.

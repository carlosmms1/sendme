---
id: 0002
title: Use Echo as Web Framework
status: accepted
date: 2025-05-15
---

# Use Echo as Web Framework

## Context and Problem Statement

To develop a performant and maintainable URL shortening service using Go, we need to choose a web framework that balances productivity, ecosystem compatibility, and community support.

## Considered Options

- **Echo:** is a mature and stable framework, closer to the Go standard library. It provides native context, better compatibility with Go idioms, and is widely used in the community.
- **Fiber:** is inspired by Express.js and offers a very familiar structure for developers coming from JavaScript/TypeScript. It is lightweight and fast but has some compatibility limitations with native Go packages due to its custom context and routing engine.

## Decision Outcome

We decided to use **Echo** as the web framework for this project, aiming for greater stability and robustness. Echo offers a mature and actively supported ecosystem, along with strong compatibility with Go’s standard library and ecosystem.

## Consequences

- The initial developer experience may be slightly less friendly for those coming from JavaScript/Express.
- We benefit from a more idiomatic Go experience and avoid compatibility issues.
- Future developers familiar with Go will onboard more easily.

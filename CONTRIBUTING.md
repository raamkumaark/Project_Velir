# Contributing to Project Velir

Thank you for contributing to Project Velir.

## Development Philosophy

Project Velir follows a documentation-first workflow.

Before implementing a feature:

1. Read the relevant documentation.
2. Confirm the architecture.
3. Implement only the requested feature.
4. Write or update tests.
5. Update documentation if necessary.

---

## Coding Standards

* Use Typed GDScript.
* Follow the existing folder structure.
* Keep gameplay systems modular.
* Prefer Resources over hardcoded values.
* Use Signals for communication.
* Avoid duplicated logic.

---

## Commit Messages

Examples:

```
feat: implement BoardManager

fix: resolve battle calculation bug

docs: update Economy System

refactor: simplify TurnManager
```

---

## Pull Requests

Every Pull Request should:

* Compile successfully
* Pass tests
* Update documentation when required
* Contain one logical feature
* Follow the project architecture

---

## Branch Strategy

```
main

↓

develop

↓

feature/*
```

Do not commit unfinished work directly to the main branch.

---

Thank you for helping build Project Velir.

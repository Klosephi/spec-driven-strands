# AWS Strands Agent Development Rules

## Overview
This document defines the development standards and practices for building AI agents using AWS Strands with Python. These rules ensure consistent, maintainable, and testable agent implementations.

## Project Structure

### Directory Layout
```
project/
├── infra/           # Infrastructure code (CDK, Terraform, etc.)
├── src/
│   ├── agents/      # Agent implementations
│   └── tools/       # Custom tools
└── tests/           # Test files
```

### Purpose
- `infra/` - AWS infrastructure as code
- `src/agents/` - Strands agent implementations using SDK patterns
- `src/tools/` - Custom Python tools (decorators, class-based, modules)
- `tests/` - Unit and integration tests

## Python Development Standards

### Environment Management
- **MUST** use a virtual environment (venv)
- **MUST** use `uv` as package manager
- **MUST** maintain `pyproject.toml` for dependencies

### Code Style
- **MUST** use Black for code formatting
- **MUST** enforce 88 character maximum line length
- **MUST** include type hints for all function parameters and return values
- **MUST** follow PEP 8 naming conventions

### Error Handling
- **MUST** use specific exception types (never bare `except:`)
- **MUST** include meaningful error messages
- **MUST** log errors at appropriate levels (DEBUG, INFO, WARNING, ERROR, CRITICAL)

### Testing Requirements
- **MUST** follow test-driven development (TDD)
- **MUST** create unit tests for all new code
- **MUST** execute existing tests before committing changes
- **MUST** maintain test coverage above 80%

## Development Workflow

### Incremental Development
- **MUST** apply changes in small, testable chunks
- **MUST** keep implementations simple (prototyping scenario)
- **MUST** break down complex features into minimal viable increments

### Planning Process
1. **MUST** explain the implementation plan before coding
2. **MUST** document the plan in a `.md` file
3. **MUST** request user approval before proceeding
4. **MUST** ensure the plan enforces these rules
5. **MUST** log progress updates in the plan file

### Change Management
- **MUST** validate all changes against these rules
- **MUST** run tests after each change
- **MUST** commit frequently with descriptive messages
- **MUST** document any rule exceptions with justification

## AWS Strands Specific Guidelines

### Agent Implementation
- **MUST** use proper Agent initialization with required parameters
- **MUST** implement tools using one of three patterns: decorators, class-based, or modules
- **SHOULD** consider A2A protocol for multi-agent communication
- **SHOULD** implement proper error handling in agent loops

### Tool Development
- **MUST** include proper docstrings for tool functions
- **MUST** use type hints for tool parameters
- **MUST** follow JSON schema generation requirements
- **SHOULD** implement both sync and async versions when applicable

## Compliance and Validation

### Rule Enforcement
- These rules are **MANDATORY** unless explicitly documented exceptions exist
- All code reviews **MUST** validate compliance with these rules
- Any rule violations **MUST** be addressed before merging

### Documentation Updates
- Rules **MAY** be updated based on project evolution
- All rule changes **MUST** be documented with rationale
- Team **MUST** be notified of rule changes

---

**Version**: 1.0  
**Last Updated**: 2025-10-07  
**Next Review**: 2025-11-07

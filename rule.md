# AWS Strands Agent Development Rules

## Overview
This document defines the development standards and practices for building AI agents using AWS Strands with Python. These rules ensure consistent, maintainable, and testable agent implementations.

## Project Structure

### Directory Layout
```
project/
├── infra/           # Infrastructure code (Notebooks for the demo)
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

### Dependency Management
- **MUST** ensure all Python dependencies are present in package manager and venv
- **MUST** add missing dependencies to `pyproject.toml` and install them
- **MUST** validate dependency compatibility before proceeding with development

### Strands Development Requirements
- **MUST** use Strands MCP to understand problem-solving approaches in Strands
- **MUST** validate if existing Strands tools can solve the problem before creating custom solutions. Check here: https://strandsagents.com/latest/documentation/docs/user-guide/concepts/tools/community-tools-package/
- **MUST** consult Strands documentation through MCP for implementation guidance
- **MUST** always use the latest version of Strands agents

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

### Code Generation Guidelines
- **MUST** generate only what was explicitly requested - no more, no less
- **MUST** be precise in implementation scope
- **MUST** ask for clarification when requirements are unclear
- **MUST NOT** make assumptions about unstated requirements
- **MUST** request additional information when needed

### Planning Process
1. **MUST** explain the implementation plan before coding
2. **MUST** document the plan in a `.md` file
3. **MUST** request user approval before proceeding
4. **MUST** ensure the plan enforces these rules and respects the Developement workflow and the Infrastructure Management
5. **MUST** log progress updates in the plan file

### Change Management
- **MUST** validate all changes against these rules
- **MUST** run tests after each change
- **MUST** commit frequently with descriptive messages
- **MUST** document any rule exceptions with justification

## Infrastructure Management

### Deployment method via Jupyter Notebooks
- **MUST** use Jupyter notebooks for infrastructure changes and deployments
- **MUST** use boto3 for AWS resource creation and management
- **MUST** execute all code inline within notebook cells
- **MUST NOT** use `%%writefile` magic commands to generate separate files

### Deployment Workflow
- **MUST** call unit tests on previously generated agent code from `src/` directory
- **MUST** deploy agent code to AWS AgentCore runtime using boto3 in notebook
- **MUST NOT** contain actual agent implementation code in notebook
- **MUST** validate deployment success before proceeding

### Notebook Responsibilities
- **MUST** execute unit tests from `tests/` directory
- **MUST** package and deploy code from `src/agents/` and `src/tools/`
- **MUST** handle AWS AgentCore deployment configuration
- **MUST** implement proper error handling for AWS API calls
- **SHOULD** log deployment progress and results

## AWS Strands Specific Guidelines

### Agent Implementation
- **MUST** use proper Agent initialization with required parameters
- **MUST** implement tools using one of three patterns: decorators, class-based, or modules
- **SHOULD** consider A2A protocol for multi-agent communication
- **SHOULD** implement proper error handling in agent loops

### Tool Development
- **MUST** Must validate existing tools before creating a new tool. https://strandsagents.com/latest/documentation/docs/user-guide/concepts/tools/community-tools-package/
- **MUST** include proper docstrings for tool functions
- **MUST** use type hints for tool parameters
- **MUST** follow JSON schema generation requirements
- **SHOULD** implement both sync and async versions when applicable

## Compliance and Validation

### Rule Enforcement
- These rules are **MANDATORY** unless explicitly documented exceptions exist
- All code reviews **MUST** validate compliance with these rules
- Any rule violations **MUST** be addressed before merging

**Version**: 1.0  
**Last Updated**: 2025-10-07  
**Next Review**: 2025-11-07

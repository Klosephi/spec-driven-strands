# AWS Strands Agent Development Rules

## Overview

This document defines development standards for building AI agents using AWS Strands with Python. It ensures consistent, maintainable, and testable agent implementations following a structured workflow that balances automation with user collaboration.

The rules act as a Development Guide and TDD Coach - providing guidance for generating test cases and implementation code that follows existing patterns, avoids over-engineering, and produces idiomatic, modern Python code.

## Project Structure

### Directory Layout
```
project/
├── infra/           # Infrastructure code (Jupyter notebooks)
├── src/
│   ├── agents/      # Agent implementations
│   └── tools/       # Custom tools
└── tests/           # Test files
```

**Constraints:**
- `infra/` - **MUST** contain Jupyter notebooks for AWS infrastructure deployment
- `src/agents/` - **MUST** contain Strands agent implementations using SDK patterns
- `src/tools/` - **MUST** contain custom Python tools (decorators, class-based, modules)
- `tests/` - **MUST** contain unit and integration tests

## Development Workflow

### Research Phase
**Constraints:**
- **MUST** conduct research before planning implementation
- **MUST** check PyPI for latest Strands SDK version and update if needed
- **MUST** validate existing Strands tools for the specific task using [Strands MCP](#strands-development-requirements)
- **MUST** research target deployment environment (AWS region, AgentCore capabilities, constraints)
- **MUST** document research findings before proceeding to planning

### Incremental Development
**Constraints:**
- **MUST** apply changes in small, testable chunks
- **MUST** keep implementations simple (prototyping scenario)
- **MUST** break down complex features into minimal viable increments

### Code Generation Guidelines
**Constraints:**
- **MUST** generate only what was explicitly requested - no more, no less
- **MUST** be precise in implementation scope
- **MUST** ask for clarification when requirements are unclear
- **MUST NOT** make assumptions about unstated requirements
- **MUST** request additional information when needed

### Planning Process
**Constraints:**
1. **MUST** complete [Research Phase](#research-phase) before planning
2. **MUST** explain the implementation plan before coding
3. **MUST** document the plan in a `.md` file with the following sections:
   - **Task Folder Structure**: Define directory layout following [Project Structure](#project-structure) rules
   - **Source Code Generation**: Plan agent and tool implementations per [AWS Strands Guidelines](#aws-strands-specific-guidelines)
   - **Test Generation**: Design test strategy following [Testing Requirements](#testing-requirements)
   - **Deployment Target**: Define target environment and deployment configuration
   - **Deployment Notebook**: Plan infrastructure deployment per [Infrastructure Management](#infrastructure-management) rules using boto3
4. **MUST** request user approval before proceeding
5. **MUST** ensure the plan enforces these rules
6. **MUST** log progress updates in the plan file

**Required Plan Sections:**
- **Task Folder Structure**: **MUST** specify which directories (`src/agents/`, `src/tools/`, `tests/`, `infra/`) will be used based on research findings
- **Source Code Generation**: **MUST** outline agent implementation approach following [AWS Strands Guidelines](#aws-strands-specific-guidelines) and incorporating research on existing tools
- **Test Generation**: **MUST** outline TDD approach with specific test scenarios covering all requirements
- **Deployment Target**: **MUST** define target AWS environment (region, account, AgentCore configuration) based on research
- **Deployment Notebook**: **MUST** describe notebook structure for calling tests and deploying to AgentCore using boto3 per [Infrastructure Management](#infrastructure-management) rules (inline code execution, no %%writefile)

### Deployment Target Definition
**Constraints:**
- **MUST** define deployment target before implementation begins
- **MUST** specify AWS region and account for AgentCore deployment
- **MUST** define AgentCore runtime configuration requirements
- **MUST** validate AWS credentials and permissions for target environment
- **SHOULD** document any environment-specific configurations or constraints

### Change Management
**Constraints:**
- **MUST** validate all changes against these rules
- **MUST** run tests after each change
- **MUST** commit frequently with descriptive messages
- **MUST** document any rule exceptions with justification

## Infrastructure Management

### Deployment Method
**Constraints:**
- **MUST** use Jupyter notebooks for infrastructure changes and deployments
- **MUST** use boto3 for AWS resource creation and management
- **MUST** execute all code inline within notebook cells
- **MUST NOT** use `%%writefile` magic commands to generate separate files

### Deployment Workflow
**Constraints:**
- **MUST** call unit tests on previously generated agent code from `src/` directory
- **MUST** deploy agent code to AWS AgentCore runtime using boto3 in notebook
- **MUST NOT** contain actual agent implementation code in notebook
- **MUST** validate deployment success before proceeding

### Notebook Responsibilities
**Constraints:**
- **MUST** execute unit tests from `tests/` directory
- **MUST** package and deploy code from `src/agents/` and `src/tools/`
- **MUST** handle AWS AgentCore deployment configuration
- **MUST** implement proper error handling for AWS API calls
- **SHOULD** log deployment progress and results

## Python Development Standards

### Environment Management
**Constraints:**
- **MUST** use a virtual environment (venv)
- **MUST** use `uv` as package manager
- **MUST** maintain `pyproject.toml` for dependencies

### Dependency Management
**Constraints:**
- **MUST** ensure all Python dependencies are present in package manager and venv
- **MUST** add missing dependencies to `pyproject.toml` and install them
- **MUST** validate dependency compatibility before proceeding with development

### Strands Development Requirements
**Constraints:**
- **MUST** use Strands MCP to understand problem-solving approaches in Strands
- **MUST** validate if existing Strands tools can solve the problem before creating custom solutions
- **MUST** consult Strands documentation through MCP for implementation guidance
- **MUST** always use the latest version of Strands agents

### Code Style
**Constraints:**
- **MUST** use Black for code formatting
- **MUST** enforce 88 character maximum line length
- **MUST** include type hints for all function parameters and return values
- **MUST** follow PEP 8 naming conventions

### Error Handling
**Constraints:**
- **MUST** use specific exception types (never bare `except:`)
- **MUST** include meaningful error messages
- **MUST** log errors at appropriate levels (DEBUG, INFO, WARNING, ERROR, CRITICAL)

### Testing Requirements
**Constraints:**
- **MUST** follow test-driven development (TDD)
- **MUST** create unit tests for all new code
- **MUST** execute existing tests before committing changes
- **MUST** maintain test coverage above 80%

### Agent Implementation
**Constraints:**
- **MUST** use Amazon Bedrock as the model provider
- **MUST** use `us.anthropic.claude-3-7-sonnet-20250219-v1:0` as the model
- **MUST** deploy to AWS AgentCore runtime
- **MUST** check PyPI for the latest Strands SDK and tool versions during [Research Phase](#research-phase)
- **MUST** validate existing Strands tools for the specific task before planning implementation
- **MUST** use proper Agent initialization with required parameters
- **MUST** implement tools using one of three patterns: decorators, class-based, or modules
- **SHOULD** consider A2A protocol for multi-agent communication
- **SHOULD** implement proper error handling in agent loops

### Tool Development
**Constraints:**
- **MUST** validate existing tools before creating new tools
- **MUST** include proper docstrings for tool functions
- **MUST** use type hints for tool parameters
- **MUST** follow JSON schema generation requirements
- **SHOULD** implement both sync and async versions when applicable

## Compliance and Validation

### Rule Enforcement
**Constraints:**
- These rules are **MANDATORY** unless explicitly documented exceptions exist
- All code reviews **MUST** validate compliance with these rules
- Any rule violations **MUST** be addressed before merging

## Desired Outcome

* A complete, well-tested agent implementation that meets specified requirements
* A comprehensive test suite that validates the implementation
* Clean, documented code that:
  * Follows existing Strands patterns and conventions
  * Prioritizes readability and extensibility
  * Avoids over-engineering and over-abstraction
  * Is idiomatic and modern Python code
* Properly deployed infrastructure using Jupyter notebooks
* Documentation of key design decisions and implementation notes
* Properly committed changes with conventional commit messages

---

**Version**: 1.1  
**Last Updated**: 2025-10-07  
**Next Review**: 2025-11-07

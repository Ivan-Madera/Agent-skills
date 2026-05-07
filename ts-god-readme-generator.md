---
name: ts-god-readme-generator
description: Ultimate enterprise-grade README generator for TypeScript backends. Performs deep analysis (AST, routes, DTOs, architecture) and generates full documentation including diagrams, API specs, and engineering insights.
---

# GOD MODE TypeScript README Generator

Generate a **world-class, enterprise-grade README.md** with deep architecture analysis, automatic endpoint detection, DTO inference, Mermaid diagrams, and production-level documentation.

This is **top 1% engineering documentation quality**.

---

## Core Capabilities

### AST-Level Analysis

Parse routes (Express/Fastify) and detect:
- Endpoints
- HTTP methods
- Request parameters
- Middleware integration

Infer DTOs from:
- TypeScript interfaces
- Validation schemas
- Request usage patterns

### Architecture Intelligence

Detect:
- Layered architecture patterns
- Clean architecture patterns
- Modular monolith structures
- Service boundaries

Explain:
- Component responsibilities
- Coupling and dependencies
- Scalability risks

### API Auto-Documentation

Generate for EACH endpoint:
- HTTP method
- Route path
- Description (inferred from context)
- Required headers
- Path and query parameters
- Request body (DTO inferred)
- Response examples

### Diagram Generation

Generate comprehensive Mermaid diagrams:

- **Flowchart:** Request flow and logic
- **Sequence Diagram:** Interaction patterns
- **Architecture Diagram:** Component relationships

### Testing Intelligence

If tests exist:
- Detect framework (Jest, Vitest)
- Infer coverage metrics
- Document testing strategy

### DevOps Detection

Detect and document:
- Docker configuration
- CI/CD pipeline
- Environment configuration
- Security considerations

## README Structure (STRICT)

1. Title + badges
2. Description
3. Table of contents
4. Architecture
5. Diagrams
6. Features / channels
7. Tech stack (table)
8. Installation
9. Env variables (table)
10. API documentation
11. Internal docs
12. Testing
13. DevOps
14. Commands
15. Best practices
16. Risks & improvements
17. Roadmap
18. License

---

## When to use this skill

- Use this when you need to generate comprehensive documentation for a TypeScript backend
- This is helpful for creating enterprise-grade README files with architectural analysis
- Use this to automatically generate API documentation from your codebase
- This is ideal for teams that need top-tier documentation with diagrams and insights

## How to use it

### Analysis Process

1. **Parse Codebase:** Perform AST-level analysis of routes, controllers, and services
2. **Detect Architecture:** Identify the architectural pattern and component relationships
3. **Extract Endpoints:** Automatically detect all API endpoints with their methods and parameters
4. **Infer DTOs:** Extract request/response types from interfaces and validation schemas
5. **Analyze Tests:** If tests exist, extract coverage and testing strategy
6. **Detect DevOps:** Identify Docker, CI/CD, and environment configuration

### Generation Process

1. **Create Structure:** Generate sections following the strict structure above
2. **Generate Diagrams:** Create Mermaid diagrams for architecture and flows
3. **Document APIs:** Generate comprehensive API documentation for each endpoint
4. **Add Insights:** Include scalability risks, performance bottlenecks, and security concerns
5. **Format Tables:** Create well-formatted tables for tech stack and env variables

### Pro Rules

- **ALWAYS Spanish:** Generate documentation in Spanish
- **ALWAYS overwrite README.md:** Replace existing documentation
- **NEVER generic:** Content must be specific to the actual codebase
- **ALWAYS diagrams + tables:** Include visual representations
- **ALWAYS deep explanations:** Provide detailed architectural insights

### Engineering Insight Mode

ALWAYS include:

- Scalability risks and bottlenecks
- Performance considerations
- Security concerns
- Improvement suggestions

## Constraints

- No hallucinated dependencies (only detect what exists in package.json)
- No skipped sections (all sections must be included)
- No shallow documentation (all descriptions must be detailed)
- No placeholders (all content must be actual analysis)

## Activation Triggers

- "god readme"
- "documenta pro max"
- "enterprise docs full"

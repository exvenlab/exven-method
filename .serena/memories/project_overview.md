# BMAD-METHOD™ Project Overview

## Purpose

BMAD-METHOD™ is a Universal AI Agent Framework for Agentic Agile Driven Development. It transforms domains with specialized AI expertise through two key innovations:

1. **Agentic Planning**: Dedicated agents (Analyst, PM, Architect) collaborate to create detailed PRDs and Architecture documents
2. **Context-Engineered Development**: Scrum Master agent transforms plans into hyper-detailed development stories for the Dev agent

## Tech Stack

- **Node.js**: v20+ required
- **JavaScript**: Mixed ES modules (.mjs) and CommonJS (.cjs, .js)
- **YAML**: Configuration format (.yaml extension required, not .yml)
- **ESLint**: Flat config with Unicorn and Node.js plugins
- **Prettier**: Code formatting with package.json plugin
- **Husky + lint-staged**: Git hook automation

## Architecture

- `bmad-core/`: Framework core with agents, workflows, templates
  - `agents/`: Individual AI agent definitions
  - `workflows/`: Workflow templates and configurations
  - `templates/`: Document and file templates
- `tools/`: Build system, CLI tools, and utilities
- `expansion-packs/`: Domain-specific extensions
- `docs/`: Documentation and user guides
- `dist/`: Built agent and team bundles for web deployment

## Development Workflow

1. **Planning Phase (Web UI)**: Use agents to create PRD and Architecture documents
2. **Development Cycle (IDE)**: SM, Dev, and QA agents collaborate through story files

Stories are stored in `docs/stories/` and contain complete context for development tasks.

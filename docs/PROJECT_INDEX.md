# BMAD-METHOD™ Project Index

## 📁 Directory Structure

### Core Framework

- **`bmad-core/`** - Framework core components
  - **`agents/`** - Individual AI agent definitions (analyst.md, dev.md, pm.md, etc.)
  - **`workflows/`** - Workflow templates and configurations
  - **`templates/`** - Document and file templates
  - **`agent-teams/`** - Team configurations and collaborative setups
  - **`tasks/`** - Predefined task definitions
  - **`checklists/`** - Quality and process checklists
  - **`data/`** - Core data files and configurations
  - **`core-config.yaml`** - Main framework configuration

### Build System & Tools

- **`tools/`** - Build system, CLI tools, and utilities
  - **`cli.js`** - Main CLI entry point
  - **`bmad-npx-wrapper.js`** - NPX wrapper for global installation
  - **`installer/`** - Installation scripts and utilities
  - **`flattener/`** - Code flattening utilities
- **`dist/`** - Built agent and team bundles for web deployment
- **`scripts/`** - Additional utility scripts

### Extensions & Documentation

- **`expansion-packs/`** - Domain-specific extensions (game dev, DevOps, etc.)
- **`docs/`** - Complete documentation suite
  - **`user-guide.md`** - Primary user documentation
  - **`core-architecture.md`** - Technical architecture deep dive
  - **`expansion-packs.md`** - Extension development guide
  - **`working-in-the-brownfield.md`** - Legacy system integration
  - **`enhanced-ide-development-workflow.md`** - IDE workflow specifics

### Configuration & Meta

- **`common/`** - Shared utilities and common code
- **`.github/`** - GitHub workflows and templates
- **`.husky/`** - Git hooks configuration
- **`.vscode/`** - VS Code workspace settings
- **`.serena/`** - Serena MCP configuration

## 🚀 Key Entry Points

### For Users

1. **`README.md`** - Project overview and quick start
2. **`docs/user-guide.md`** - Complete workflow walkthrough
3. **`bmad-core/agents/`** - Available AI agents

### For Developers

1. **`package.json`** - Project dependencies and scripts
2. **`tools/cli.js`** - Main CLI implementation
3. **`eslint.config.mjs`** - Code quality configuration
4. **`prettier.config.mjs`** - Code formatting rules

## 📋 Essential Commands

### Development

```bash
npm run fix              # Format + lint fix (recommended before commit)
npm run build            # Build all web bundles
npm run validate         # Validate project structure
npm run list:agents      # List available agents
```

### Installation

```bash
npm run install:bmad     # Install BMAD in destination folder
npx bmad-method install  # Install BMAD in current project
```

## 🏗️ Architecture Overview

### Two-Phase Development Approach

1. **Planning Phase (Web UI)**
   - Analyst, PM, and Architect agents collaborate
   - Creates detailed PRDs and Architecture documents
   - Human-in-the-loop refinement

2. **Development Cycle (IDE)**
   - Scrum Master transforms plans into detailed stories
   - Dev and QA agents work through story files
   - Complete context embedded in each story

### Key Innovations

- **Context-Engineered Development**: Stories contain full implementation context
- **Agentic Planning**: Specialized agents for different planning roles
- **Brownfield Integration**: Works with existing codebases and legacy systems

## 📊 File Types & Extensions

- **`.yaml`** - Configuration files (required, not `.yml`)
- **`.mjs`** - ES modules
- **`.cjs`** - CommonJS modules
- **`.js`** - Regular JavaScript
- **`.md`** - Documentation and agent definitions

## 🎯 Quality Standards

- Zero ESLint warnings tolerance
- Prettier formatting with 100 character limit
- Husky pre-commit hooks enforce quality
- Node.js v20+ requirement
- MIT License

## 🔧 Tech Stack

- **Runtime**: Node.js v20+
- **Languages**: JavaScript (ES modules + CommonJS)
- **Config**: YAML
- **Quality**: ESLint + Prettier + Husky
- **Build**: Custom CLI tools
- **Version Control**: Git with automated hooks

## 📚 Learning Path

1. **Start Here**: `README.md` → `docs/user-guide.md`
2. **Understand Agents**: Browse `bmad-core/agents/`
3. **Try Examples**: Check `expansion-packs/` for domain examples
4. **Deep Dive**: `docs/core-architecture.md`
5. **Contribute**: `CONTRIBUTING.md` and `docs/how-to-contribute-with-pull-requests.md`

## 🌟 Expansion Packs

The framework supports domain-specific extensions in `expansion-packs/`:

- Game development workflows
- DevOps and infrastructure automation
- Creative writing and content creation
- Business strategy and planning
- Educational content development

Each expansion pack demonstrates how to adapt BMAD-METHOD™ for specific domains beyond software development.

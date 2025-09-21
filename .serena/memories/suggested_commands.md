# Essential Development Commands

## Code Quality (Run Before Committing)

```bash
npm run fix              # Format + lint fix (recommended)
npm run format           # Format code with Prettier
npm run lint             # Lint with ESLint (must pass with 0 warnings)
npm run lint:fix         # Fix linting issues automatically
npm run validate         # Validate project structure
```

## Build System

```bash
npm run build            # Build all web bundles (agents and teams)
npm run build:agents     # Build only agent bundles
npm run build:teams      # Build only team bundles
npm run list:agents      # List available agents
```

## Installation and Updates

```bash
npm run install:bmad     # Install/update BMAD in destination folder
npx bmad-method install  # Install BMAD in current project (NPX)
```

## Pre-commit Requirements

- Husky runs lint-staged automatically
- All files must pass linting with 0 warnings
- Format and lint fixes applied automatically to staged files

## Testing and Release

```bash
npm run pre-release      # Run validation, format check, and lint
npm run version:patch    # Bump patch version
npm run version:minor    # Bump minor version
npm run version:major    # Bump major version
```

## System Commands (Darwin/macOS)

- `ls`: List directory contents
- `find`: Search for files and directories
- `grep`: Search text in files (consider using `rg` ripgrep if available)
- `git`: Version control operations
- `cd`: Change directory
- `chmod`: Change file permissions

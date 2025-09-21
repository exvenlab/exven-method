# Code Style and Conventions

## File Extensions

- Use `.yaml` for YAML files (enforced by ESLint, not `.yml`)
- Use `.mjs` for ES modules
- Use `.cjs` for CommonJS
- Use `.js` for regular JavaScript

## Linting Rules

- ESLint flat config with 0 warnings tolerance
- Prettier formatting with 100 character line width
- YAML files prefer double quotes, single quotes allowed to avoid escaping
- Console usage allowed (CLI tool context)

## Code Style Guidelines

- Unicorn plugin enforces modern best practices
- Node.js plugin for proper Node.js patterns
- Mixed ESM and CommonJS support
- Consistent function scoping
- Prefer ternary operators where appropriate

## Naming Conventions

- Use descriptive variable and function names
- Avoid abbreviations (unicorn/prevent-abbreviations disabled for this project)
- Use kebab-case for file names in general
- Use camelCase for JavaScript variables and functions

## Project-Specific Rules

- Console statements are allowed (CLI tool context)
- Empty mapping values allowed in workflow YAML files
- CommonJS patterns allowed in tools/ directory
- Relaxed rules for internal scripts under tools/

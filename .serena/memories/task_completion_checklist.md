# Task Completion Checklist

## Before Committing Code Changes

1. **Format and Lint**: Run `npm run fix` to format and lint fix all issues
2. **Validate Structure**: Run `npm run validate` to check project structure
3. **Zero Warnings**: Ensure `npm run lint` passes with 0 warnings
4. **Build Success**: Run `npm run build` if build artifacts are needed
5. **Pre-commit Hooks**: Husky will automatically run lint-staged on commit

## Development Workflow Steps

1. Make code changes
2. Run `npm run fix` (format + lint fix)
3. Run `npm run validate` (project structure validation)
4. Build if needed: `npm run build`
5. Commit changes (pre-commit hooks verify everything passes)

## Quality Gates

- All ESLint rules must pass with 0 warnings
- Prettier formatting must be applied
- YAML files must use .yaml extension
- Code must follow project conventions
- No breaking changes without proper documentation

## Release Preparation

- Run `npm run pre-release` before any release
- Update version numbers with appropriate npm scripts
- Ensure all tests pass (if applicable)
- Update documentation as needed

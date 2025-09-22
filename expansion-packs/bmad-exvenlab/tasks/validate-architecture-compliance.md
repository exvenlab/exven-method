# validate-architecture-compliance

Semantic validation to ensure implementation strictly follows architecture standards loaded from devLoadAlwaysFiles.

## Overview

This task enables dev agents to validate their implementation against architecture standards using Serena semantic analysis, ensuring consistent adherence to project architectural guidelines.

## Prerequisites

- Serena MCP server active with [editing, interactive] modes
- Dev agent with architectureShardedLocation documents loaded during activation
- Implementation code available for validation
- Architecture documents accessible in project

## Architecture Compliance Workflow

### Phase 1: Architecture Standards Discovery

1. **Load Architecture Context**

   ```
   Reference ALL architecture documents from architectureShardedLocation loaded during activation:
   - All .md files discovered in docs/architecture/ directory
   - Dynamic loading ensures no architecture standards are missed
   - Includes both standard and project-specific architecture documents
   ```

2. **Extract Compliance Rules**
   ```
   From ALL loaded architecture documents, identify:
   - Coding patterns and conventions required
   - Technology stack constraints and approved libraries
   - File organization and naming standards
   - API design patterns and interfaces
   - Testing requirements and patterns
   - Security guidelines and requirements
   - Deployment and infrastructure standards
   - Any project-specific architectural requirements
   ```

### Phase 2: Implementation Analysis

1. **Code Pattern Validation**

   ```
   Use search_for_pattern to validate:
   - Implementation follows required coding patterns
   - Naming conventions match architecture standards
   - File organization adheres to source tree structure
   - API patterns match architectural guidelines
   ```

2. **Technology Stack Compliance**
   ```
   Use find_symbol to verify:
   - Only approved frameworks and libraries are used
   - Import statements match tech stack requirements
   - Dependencies align with architecture constraints
   - No prohibited technologies or patterns present
   ```

### Phase 3: Structural Compliance Check

1. **Module Organization Validation**

   ```
   Use get_symbols_overview to assess:
   - File structure follows source tree guidelines
   - Module boundaries respect architectural layers
   - Component organization matches standards
   - Interface design follows patterns
   ```

2. **Integration Pattern Compliance**
   ```
   Use find_referencing_symbols to validate:
   - Inter-module communication follows patterns
   - API usage matches architectural guidelines
   - Dependency injection follows standards
   - Error handling patterns are consistent
   ```

## Validation Categories

### Critical Compliance (Must Fix)

- **Technology Stack Violations**: Use of prohibited libraries/frameworks
- **Architectural Layer Violations**: Breaking layer boundaries or dependencies
- **Security Pattern Violations**: Not following security guidelines
- **API Contract Violations**: Breaking established interface patterns

### Standard Compliance (Should Fix)

- **Coding Standard Violations**: Style, naming, or pattern deviations
- **File Organization Issues**: Incorrect placement or naming
- **Testing Pattern Deviations**: Not following testing standards
- **Documentation Violations**: Missing or incorrect documentation

### Style Compliance (Nice to Fix)

- **Code Style Inconsistencies**: Minor formatting or style issues
- **Comment Standards**: Documentation improvements
- **Naming Optimizations**: Better naming that follows guidelines
- **Code Organization**: Improved structure within standards

## Compliance Report Format

### Architecture Compliance Report

```markdown
# Architecture Compliance Validation

## Implementation: [Feature/Component Name]

### Compliance Summary

- **Overall Status**: [COMPLIANT/VIOLATIONS/CRITICAL]
- **Critical Issues**: [Count] - Must fix before approval
- **Standard Issues**: [Count] - Should fix for quality
- **Style Issues**: [Count] - Nice to fix for consistency

## Architecture Standards Checked

### Dynamic Architecture Document Coverage

- **Documents Loaded**: [List all architecture documents from architectureShardedLocation]
- **Standards Applied**: [Total count of standards checked]
- **Custom Requirements**: [Project-specific standards identified]

### Coding Standards Compliance

- **Pattern Adherence**: [PASS/FAIL] - [Details from coding standards docs]
- **Naming Conventions**: [PASS/FAIL] - [Details from style guides]
- **Code Organization**: [PASS/FAIL] - [Details from structure docs]

### Tech Stack Compliance

- **Approved Libraries**: [PASS/FAIL] - [Details from tech stack docs]
- **Framework Usage**: [PASS/FAIL] - [Details from framework guidelines]
- **Dependency Management**: [PASS/FAIL] - [Details from dependency policies]

### Architectural Pattern Compliance

- **API Standards**: [PASS/FAIL] - [Details from API design docs]
- **Security Guidelines**: [PASS/FAIL] - [Details from security docs]
- **Testing Standards**: [PASS/FAIL] - [Details from testing docs]
- **Deployment Patterns**: [PASS/FAIL] - [Details from deployment docs]

## Critical Violations (Must Fix)

### Technology Stack Violations

- **Issue**: [Description of violation]
- **Location**: [File/function where found]
- **Required Action**: [Specific fix needed]
- **Architecture Reference**: [Section of architecture doc violated]

### Architectural Pattern Violations

- **Issue**: [Description of violation]
- **Location**: [File/function where found]
- **Required Action**: [Specific fix needed]
- **Architecture Reference**: [Section of architecture doc violated]

## Standard Violations (Should Fix)

### Coding Standard Issues

- **Issue**: [Description of issue]
- **Location**: [File/function where found]
- **Recommended Action**: [Suggested improvement]
- **Standard Reference**: [Relevant standard]

### Organization Issues

- **Issue**: [Description of issue]
- **Location**: [File/directory affected]
- **Recommended Action**: [Suggested improvement]
- **Standard Reference**: [Relevant standard]

## Style Recommendations (Nice to Fix)

### Code Style Improvements

- **Suggestion**: [Improvement suggestion]
- **Location**: [Where to apply]
- **Benefit**: [Why this improves code quality]

## Compliance Validation Details

### Semantic Analysis Results

**Pattern Analysis:**

- **Search Patterns Used**: [List of patterns searched]
- **Matches Found**: [Results of pattern matching]
- **Compliance Assessment**: [How patterns align with standards]

**Symbol Analysis:**

- **Symbols Analyzed**: [Key symbols checked]
- **Dependencies Validated**: [Dependency compliance]
- **Interface Compliance**: [API/interface alignment]

**Structure Analysis:**

- **Module Organization**: [Structure validation results]
- **Layer Compliance**: [Architectural layer adherence]
- **Integration Patterns**: [Inter-module communication validation]

## Remediation Plan

### Immediate Actions (Critical)

1. **[Issue]**: [Specific action needed]
2. **[Issue]**: [Specific action needed]

### Recommended Actions (Standard)

1. **[Issue]**: [Specific action needed]
2. **[Issue]**: [Specific action needed]

### Optional Improvements (Style)

1. **[Suggestion]**: [Improvement opportunity]
2. **[Suggestion]**: [Improvement opportunity]

## Implementation Guidance

### Compliant Patterns

- **Approved Patterns**: [Examples from codebase that follow standards]
- **Reference Implementations**: [Good examples to follow]
- **Best Practices**: [Recommended approaches]

### Common Pitfalls

- **Avoid**: [Common mistakes that violate standards]
- **Watch For**: [Areas requiring special attention]
- **Validate**: [Checkpoints for compliance]
```

## Integration with Dev Workflow

### Before Implementation

```
Use validate-architecture-compliance to:
- Understand architectural constraints for feature
- Identify approved patterns and technologies
- Plan implementation approach within guidelines
```

### During Implementation

```
Use throughout development process to:
- Validate each component against standards
- Ensure consistency with architectural patterns
- Catch violations early in development cycle
```

### Before Code Review

```
Use as final validation to:
- Ensure implementation meets all architectural standards
- Provide compliance report for reviewers
- Address any violations before review submission
```

## Semantic Analysis Techniques

### Pattern Matching for Standards

```
Use search_for_pattern to find:
- Coding pattern violations (incorrect naming, structure)
- Technology usage violations (prohibited libraries)
- Architectural pattern violations (layer breaking)
```

### Symbol Analysis for Compliance

```
Use find_symbol to validate:
- Approved API patterns and interfaces
- Correct dependency injection patterns
- Proper error handling implementations
```

### Structure Analysis for Organization

```
Use get_symbols_overview to check:
- File organization compliance
- Module boundary adherence
- Component structure alignment
```

### Reference Analysis for Dependencies

```
Use find_referencing_symbols to validate:
- Inter-module dependency compliance
- API usage pattern adherence
- Integration pattern consistency
```

## Success Criteria

- All critical violations identified and addressed
- Standard violations documented with remediation plan
- Implementation aligns with all architectural guidelines
- Code follows established patterns and conventions
- Technology usage complies with approved stack
- File organization matches source tree standards

## Notes

- This validation runs automatically in enhanced develop-story workflow
- Focuses on architectural compliance, not functional correctness
- Provides specific, actionable guidance for remediation
- Integrates seamlessly with existing development process
- Supports consistent code quality across development team

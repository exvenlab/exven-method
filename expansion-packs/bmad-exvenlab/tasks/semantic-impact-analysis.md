# semantic-impact-analysis

Comprehensive semantic analysis of code changes impact using Serena MCP tools for informed decision making.

## Overview

This task enables agents to understand the full impact of proposed changes before implementation, identifying potential breaking changes, affected components, and required updates across the codebase.

## Prerequisites

- Serena MCP server active
- Agent in [planning, interactive] modes (read-only analysis)
- Target codebase available for semantic analysis
- Clear scope of proposed changes defined

## Impact Analysis Workflow

### Phase 1: Change Scope Discovery

1. **Target Component Analysis**

   ```
   Use find_symbol to understand:
   - Current implementation of components to be changed
   - Method signatures and interfaces that might be affected
   - Data structures and models involved
   - Public APIs and contracts exposed
   ```

2. **Dependency Mapping**
   ```
   Use find_referencing_symbols to identify:
   - All components that depend on targets to be changed
   - Direct and indirect usage patterns
   - Integration points and API consumers
   - Test files that might be affected
   ```

### Phase 2: Impact Assessment

1. **Breaking Change Analysis**

   ```
   Use find_referencing_symbols to assess:
   - Which calling code might break with proposed changes
   - Interface compatibility issues
   - Data structure breaking changes
   - API contract modifications
   ```

2. **Cascade Effect Identification**
   ```
   Use search_for_pattern to find:
   - Similar patterns that might need consistent updates
   - Related configurations or constants
   - Documentation that references changing components
   - Migration scripts or setup code affected
   ```

### Phase 3: Risk and Effort Assessment

1. **Change Complexity Analysis**

   ```
   Use get_symbols_overview to understand:
   - Architecture patterns that constrain changes
   - Integration complexity across modules
   - Testing requirements and coverage implications
   - Deployment and migration considerations
   ```

2. **Ripple Effect Mapping**
   ```
   For each affected component, use find_referencing_symbols to:
   - Identify secondary dependencies
   - Map the full dependency chain
   - Understand transitive impacts
   - Assess test coverage gaps
   ```

## Analysis Categories

### Critical Impact (Must Address)

- **Breaking Changes**: Changes that will break existing functionality
- **API Modifications**: Public interface changes affecting consumers
- **Data Model Changes**: Schema or structure modifications
- **Security Implications**: Changes affecting authentication/authorization

### Moderate Impact (Should Consider)

- **Performance Implications**: Changes affecting system performance
- **Integration Points**: Modifications to external service interfaces
- **Configuration Changes**: Updates to settings or environment variables
- **Documentation Updates**: Technical documentation requiring updates

### Low Impact (Monitor)

- **Internal Refactoring**: Changes that don't affect external interfaces
- **Code Style Updates**: Formatting or naming improvements
- **Comment Updates**: Documentation improvements in code
- **Test Improvements**: Enhanced test coverage or test quality

## Impact Report Format

### Semantic Impact Analysis Report

```markdown
# Semantic Impact Analysis: [Change Description]

## Executive Summary

- **Overall Risk Level**: [High/Medium/Low]
- **Components Affected**: [Number] direct, [Number] indirect
- **Breaking Changes**: [Yes/No] - [Count if any]
- **Estimated Effort**: [High/Medium/Low]

## Change Scope Analysis

### Target Components

- **Primary Targets**: [List of components being modified]
- **Interfaces Modified**: [APIs, classes, functions being changed]
- **Data Structures Affected**: [Models, schemas, types being changed]

### Direct Dependencies

- **Immediate Consumers**: [Components directly using targets]
- **API Clients**: [External or internal API consumers]
- **Test Dependencies**: [Test files directly testing targets]

### Indirect Dependencies

- **Transitive Dependencies**: [Components affected through dependency chain]
- **Configuration Dependencies**: [Settings, environment variables affected]
- **Documentation Dependencies**: [Docs requiring updates]

## Breaking Change Assessment

### Critical Breaking Changes

- [List changes that will break existing functionality]
- **Affected Components**: [List with specific impact]
- **Mitigation Required**: [Specific actions needed]

### Interface Compatibility Issues

- [List API/interface changes that affect consumers]
- **Backward Compatibility**: [Assessment and recommendations]
- **Migration Strategy**: [Approach for affected consumers]

## Risk Assessment

### High Risk Areas

- **Components**: [List high-risk affected components]
- **Reasoning**: [Why these are high risk]
- **Mitigation**: [Recommended risk mitigation strategies]

### Testing Impact

- **Tests Requiring Updates**: [List of test files needing changes]
- **New Tests Required**: [Testing gaps created by changes]
- **Coverage Implications**: [Impact on test coverage metrics]

## Implementation Recommendations

### Phased Approach Suggestion

1. **Phase 1**: [Preparatory changes]
2. **Phase 2**: [Core changes]
3. **Phase 3**: [Cleanup and optimization]

### Change Sequence Optimization

- **Prerequisites**: [Changes that must happen first]
- **Parallel Opportunities**: [Changes that can happen simultaneously]
- **Dependencies**: [Required order of operations]

### Risk Mitigation Strategies

- **Feature Flags**: [Where to use feature toggles]
- **Gradual Rollout**: [Phased deployment recommendations]
- **Rollback Plan**: [Strategy for reverting if needed]

## Effort Estimation Factors

### Development Effort

- **Core Changes**: [Estimated effort for primary modifications]
- **Dependency Updates**: [Effort for updating affected components]
- **Test Updates**: [Effort for test modifications and new tests]

### Validation Effort

- **Integration Testing**: [Testing requirements for integration points]
- **Performance Testing**: [Performance validation needs]
- **Security Review**: [Security implications requiring review]

## Monitoring and Validation Plan

### Success Metrics

- [How to measure successful implementation]
- [Performance indicators to monitor]
- [Functionality validation checkpoints]

### Post-Implementation Monitoring

- [Systems to monitor after deployment]
- [Metrics to track for early issue detection]
- [Rollback triggers and conditions]

## Appendix: Detailed Analysis

### Component Dependency Map
```

[Visual or detailed text representation of dependency relationships]

```

### Semantic Analysis Details
- **Symbol Analysis Results**: [Detailed findings from find_symbol analysis]
- **Reference Analysis Results**: [Detailed findings from find_referencing_symbols]
- **Pattern Analysis Results**: [Detailed findings from search_for_pattern]
```

## Use Cases

### Before Major Refactoring

- Assess impact of architectural changes
- Identify all affected components
- Plan migration strategy
- Estimate effort and timeline

### Before API Changes

- Identify all API consumers
- Assess breaking change implications
- Plan backward compatibility strategy
- Coordinate with dependent teams

### Before Library Updates

- Understand dependency impacts
- Identify affected integrations
- Plan testing strategy
- Assess security implications

### Before Feature Development

- Understand integration points
- Identify reusable components
- Assess complexity and effort
- Plan development approach

## Success Criteria

- Complete mapping of change impact
- Identification of all breaking changes
- Clear risk assessment and mitigation plan
- Actionable implementation recommendations
- Effort estimation for planning purposes

## Integration with BMAD Workflow

### SM Agent Usage

- Run before story creation for complex features
- Validate story feasibility and effort estimates
- Identify story dependencies and sequencing

### Architect Agent Usage

- Assess architectural change implications
- Validate design decisions against existing code
- Plan system evolution strategies

### Dev Agent Usage

- Understand implementation scope before coding
- Identify potential integration issues early
- Plan development approach and testing strategy

## Notes

- This analysis complements but doesn't replace code review
- Focuses on semantic understanding of change impact
- Provides data-driven insights for technical decisions
- Supports risk-informed development planning

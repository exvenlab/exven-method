# validate-story-semantic

Semantic validation of user stories to ensure technical accuracy and implementability.

## Overview

This task enables PO agents to validate user stories against the actual codebase, ensuring stories reference real code structures and are technically feasible.

## Prerequisites

- Serena MCP server active
- Agent in [planning, interactive] modes (read-only analysis)
- Story file available for validation

## Validation Workflow

### Phase 1: Technical Reference Validation

1. **Code Structure Verification**

   ```
   Use find_symbol to verify:
   - Referenced APIs, classes, or functions actually exist
   - Method signatures match story assumptions
   - Data structures align with story requirements
   - Integration points are valid
   ```

2. **System Capability Check**
   ```
   Use get_symbols_overview to confirm:
   - Required functionality is available in the system
   - Story assumptions about system capabilities are correct
   - Integration points exist and are accessible
   ```

### Phase 2: Dependency Analysis

1. **Story Interdependency Assessment**

   ```
   Use find_referencing_symbols to identify:
   - Which other code/features this story might affect
   - Dependencies that must be completed first
   - Potential conflicts with parallel development
   - Critical integration points
   ```

2. **Implementation Path Validation**
   ```
   Use search_for_pattern to find:
   - Similar implementations for reference
   - Existing patterns that should be followed
   - Potential reusable components
   - Established conventions
   ```

### Phase 3: Consistency and Quality Check

1. **Pattern Alignment**

   ```
   Use search_for_pattern to ensure:
   - Story follows established UI/UX patterns
   - API usage aligns with existing conventions
   - Data handling matches current approaches
   - Error handling follows established patterns
   ```

2. **Acceptance Criteria Validation**
   ```
   Verify acceptance criteria against:
   - Actual API capabilities and limitations
   - Existing user interface components
   - Current data validation rules
   - System performance characteristics
   ```

## Validation Checklist

### Technical Accuracy

- [ ] All referenced APIs/classes/functions exist in codebase
- [ ] Method signatures and parameters are correct
- [ ] Data structures and models are accurately referenced
- [ ] Integration points are valid and accessible

### Implementation Feasibility

- [ ] Required functionality exists or can be reasonably implemented
- [ ] No architectural constraints prevent implementation
- [ ] Dependencies are identified and manageable
- [ ] Story scope is appropriate for system capabilities

### Consistency and Standards

- [ ] Story follows established patterns and conventions
- [ ] Acceptance criteria align with system capabilities
- [ ] User interface references match existing components
- [ ] Error handling and validation follow current practices

### Dependency Management

- [ ] Prerequisites and dependencies are identified
- [ ] No conflicts with other stories or parallel development
- [ ] Implementation order is logical and feasible
- [ ] Critical integration points are addressed

## Validation Report Format

### Story Validation Summary

```markdown
# Story Validation Report: [Story ID/Title]

## Technical Validation Results

- **Status**: [PASS/CONCERNS/FAIL]
- **Technical Accuracy**: [Assessment of technical references]
- **Implementation Feasibility**: [Assessment of feasibility]

## Identified Issues

### Critical Issues (Must Fix)

- [List of issues that prevent implementation]

### Concerns (Should Address)

- [List of issues that could cause problems]

### Recommendations (Nice to Have)

- [Suggestions for improvement]

## Dependencies and Sequencing

- **Prerequisites**: [What must be done first]
- **Parallel Concerns**: [Conflicts with other work]
- **Integration Points**: [Critical dependencies]

## Implementation Guidance

- **Existing Patterns**: [Similar implementations to reference]
- **Reusable Components**: [Available utilities and components]
- **Technical Approach**: [Recommended implementation strategy]

## Validation Decision

- [ ] **APPROVED**: Story is technically sound and ready for development
- [ ] **APPROVED WITH CONDITIONS**: Story approved with specific conditions
- [ ] **NEEDS REVISION**: Story requires changes before approval
- [ ] **REJECTED**: Story is not technically feasible as written
```

## Common Validation Scenarios

### API Reference Validation

```yaml
scenario: Story references specific API endpoints
validation_steps:
  - Use find_symbol to locate API endpoint definition
  - Verify method signature and parameters
  - Check authentication and authorization requirements
  - Validate response format and error handling
```

### User Interface Validation

```yaml
scenario: Story describes UI changes or new components
validation_steps:
  - Use search_for_pattern to find similar UI components
  - Verify component library capabilities
  - Check responsive design considerations
  - Validate accessibility requirements
```

### Data Model Validation

```yaml
scenario: Story involves data creation, modification, or display
validation_steps:
  - Use find_symbol to locate relevant data models
  - Verify field types and validation rules
  - Check database constraints and relationships
  - Validate data migration requirements
```

## Success Criteria

- All technical references in story are validated
- Implementation feasibility is confirmed
- Dependencies and risks are identified
- Clear guidance provided for development team

## Notes

- This validation complements but doesn't replace traditional story review
- Focuses on technical accuracy and implementability
- Provides concrete feedback based on actual codebase
- Supports better story quality and development efficiency

# analyze-codebase-for-product

Semantic codebase analysis for informed product management and strategic decision making.

## Overview

This task enables PM and PO agents to understand the technical reality of the codebase for better product decisions, feature scoping, and story creation.

## Prerequisites

- Serena MCP server active
- Agent in [planning, interactive] modes (read-only analysis)
- Target project/codebase specified

## Analysis Workflow

### Phase 1: Architecture Understanding

1. **High-Level Structure Analysis**

   ```
   Use get_symbols_overview to understand:
   - Overall application architecture (MVC, microservices, etc.)
   - Main modules and their purposes
   - Key integration points and APIs
   - Technology stack and patterns in use
   ```

2. **Feature Landscape Mapping**
   ```
   Use search_for_pattern to identify:
   - Existing feature implementations
   - Common patterns and conventions
   - API endpoints and data models
   - User-facing functionality
   ```

### Phase 2: Technical Feasibility Assessment

1. **Implementation Complexity Analysis**

   ```
   Use find_symbol to assess:
   - Complexity of existing similar features
   - Required integration points
   - Dependencies and constraints
   - Available utilities and frameworks
   ```

2. **Impact and Dependency Analysis**
   ```
   Use find_referencing_symbols to understand:
   - How features interconnect
   - Potential breaking changes
   - Cross-feature dependencies
   - Critical system components
   ```

### Phase 3: Product Intelligence Gathering

1. **Feature Similarity Research**

   ```
   Use search_for_pattern to find:
   - Similar existing features for effort estimation
   - Reusable components and patterns
   - Implementation approaches for reference
   - Technical precedents
   ```

2. **Technical Debt Assessment**
   ```
   Identify areas of:
   - Code duplication that could affect new features
   - Legacy patterns that constrain new development
   - Performance bottlenecks relevant to feature planning
   - Architecture limitations for product roadmap
   ```

## Product Management Applications

### For PM Agent (Feature Planning)

1. **Informed PRD Creation**
   - Base feature requirements on actual technical capabilities
   - Include realistic technical constraints in specifications
   - Reference existing patterns for consistency

2. **Effort Estimation Enhancement**
   - Understand implementation complexity through code analysis
   - Identify reusable components to reduce development time
   - Assess technical risk factors for accurate scoping

3. **Strategic Decision Support**
   - Evaluate technical debt impact on feature development
   - Assess architectural readiness for planned features
   - Inform build vs. buy decisions with technical understanding

### For PO Agent (Story Quality)

1. **Story Technical Validation**
   - Ensure stories reference actual code structures
   - Validate acceptance criteria against existing APIs
   - Check story feasibility against current architecture

2. **Dependency Identification**
   - Understand technical dependencies between stories
   - Identify prerequisite technical work
   - Plan story sequencing based on code dependencies

3. **Quality Assurance**
   - Ensure stories align with existing patterns
   - Validate technical assumptions in acceptance criteria
   - Check consistency across related stories

## Output Format

### Technical Landscape Report

```markdown
# Codebase Analysis for Product Planning

## Architecture Overview

- **Primary Architecture Pattern**: [MVC/Microservices/etc.]
- **Key Technologies**: [Languages, frameworks, databases]
- **Main Modules**: [Core business logic areas]

## Feature Implementation Patterns

- **Common Patterns**: [How features are typically implemented]
- **API Conventions**: [REST/GraphQL patterns, naming conventions]
- **Data Flow**: [How data moves through the system]

## Technical Constraints and Opportunities

- **Constraints**: [Limitations that affect feature development]
- **Opportunities**: [Existing capabilities that can be leveraged]
- **Reusable Components**: [Available utilities and frameworks]

## Effort Estimation Factors

- **High Complexity Areas**: [Parts of system that are complex to modify]
- **Low Complexity Areas**: [Areas where changes are straightforward]
- **Dependencies**: [Critical integration points to consider]

## Recommendations for Product Planning

- **Feature Prioritization**: [Technical factors affecting priority]
- **Implementation Approach**: [Suggested technical strategies]
- **Risk Mitigation**: [Technical risks and mitigation strategies]
```

## Success Criteria

- Complete understanding of technical landscape
- Actionable insights for product decisions
- Clear constraints and opportunities identified
- Realistic effort estimation factors documented

## Notes

- This is a read-only analysis task
- Focuses on product management needs, not detailed technical implementation
- Provides business-relevant technical insights
- Supports informed product planning and story creation

# load-architecture-standards

Dynamic discovery and loading of all architecture standards from architectureShardedLocation for development guidance.

## Overview

This task enables dev agents to automatically discover and load all architecture documents from the configured architectureShardedLocation directory, providing comprehensive and up-to-date development standards.

## Prerequisites

- Serena MCP server active with [editing, interactive] modes
- Project with valid config.yaml containing architectureShardedLocation
- Architecture documents available in sharded location
- Understanding of project configuration structure

## Dynamic Architecture Loading Workflow

### Phase 1: Configuration Discovery

1. **Read Project Configuration**

   ```
   Load and parse {root}/config.yaml to extract:
   - architectureShardedLocation path (typically docs/architecture)
   - architectureFile main document location
   - architectureVersion for version tracking
   - Any custom architecture-related configurations
   ```

2. **Validate Configuration**
   ```
   Verify configuration contains required fields:
   - architectureShardedLocation is defined and valid
   - Path exists and is accessible
   - Directory contains architecture documents
   ```

### Phase 2: Architecture Document Discovery

1. **Directory Scanning**

   ```
   Use list_dir tool to discover:
   - All .md files in architectureShardedLocation directory
   - Subdirectories containing additional architecture docs
   - File modification dates for freshness tracking
   - Document hierarchy and organization
   ```

2. **Document Classification**
   ```
   Categorize discovered architecture documents:
   - coding-standards.md (code style, patterns, conventions)
   - tech-stack.md (approved technologies, frameworks, libraries)
   - source-tree.md (file organization, module structure)
   - api-standards.md (API design patterns, interfaces)
   - testing-standards.md (testing patterns, requirements)
   - security-guidelines.md (security patterns, requirements)
   - deployment-standards.md (deployment, infrastructure patterns)
   - [custom documents based on project needs]
   ```

### Phase 3: Content Loading and Processing

1. **Sequential Document Loading**

   ```
   For each discovered architecture document:
   - Load full content using read_file tool
   - Extract key standards and requirements
   - Identify compliance rules and patterns
   - Note any cross-references between documents
   ```

2. **Standards Consolidation**
   ```
   Process loaded content to create unified standards reference:
   - Merge related standards from multiple documents
   - Resolve any conflicts between documents
   - Create priority hierarchy for competing standards
   - Generate quick-reference compliance checklist
   ```

### Phase 4: Development Context Preparation

1. **Create Standards Summary**

   ```
   Generate consolidated view of all standards:
   - Critical requirements that must be followed
   - Preferred patterns and approaches
   - Prohibited technologies or patterns
   - Project-specific guidelines and exceptions
   ```

2. **Prepare Validation Context**
   ```
   Create validation reference for compliance checking:
   - Search patterns for automated compliance checking
   - Symbol patterns for technology validation
   - File organization requirements
   - API and interface standards
   ```

## Loading Report Format

### Architecture Standards Loading Report

```markdown
# Architecture Standards Loading Report

## Configuration Summary

- **Architecture Location**: [architectureShardedLocation path]
- **Main Architecture File**: [architectureFile if specified]
- **Version**: [architectureVersion if specified]
- **Loading Timestamp**: [current timestamp]

## Discovered Architecture Documents

### Core Standards Documents

- **coding-standards.md**: [Found/Not Found] - [Brief summary if found]
- **tech-stack.md**: [Found/Not Found] - [Brief summary if found]
- **source-tree.md**: [Found/Not Found] - [Brief summary if found]

### Additional Architecture Documents

- **[document-name.md]**: [Brief summary of content and purpose]
- **[document-name.md]**: [Brief summary of content and purpose]

## Consolidated Standards Summary

### Critical Requirements (Must Follow)

- [List of non-negotiable standards from all documents]
- [Technology restrictions and requirements]
- [Security and compliance requirements]

### Preferred Patterns (Should Follow)

- [Recommended coding patterns and conventions]
- [Preferred frameworks and libraries]
- [API design patterns and standards]

### Prohibited Practices (Must Avoid)

- [Explicitly prohibited technologies or patterns]
- [Anti-patterns to avoid]
- [Deprecated approaches]

### Project-Specific Guidelines

- [Custom standards specific to this project]
- [Exceptions to general standards]
- [Special requirements or considerations]

## Validation Patterns Prepared

### Compliance Search Patterns

- **Coding Standards**: [List of patterns for automated checking]
- **Technology Usage**: [Patterns to validate approved tech stack]
- **File Organization**: [Patterns to check source tree compliance]

### Symbol Validation Patterns

- **Approved Libraries**: [Symbol patterns for allowed dependencies]
- **API Patterns**: [Interface and API compliance patterns]
- **Security Patterns**: [Required security implementation patterns]

## Document Cross-References

### Inter-Document Dependencies

- [How documents reference each other]
- [Conflicts resolved between documents]
- [Priority hierarchy for competing standards]

### Version Consistency

- [Version alignment across documents]
- [Update recommendations if versions inconsistent]
- [Freshness assessment of loaded standards]

## Development Readiness Status

- **Standards Loaded**: [Count] documents successfully processed
- **Critical Standards**: [Complete/Incomplete]
- **Validation Patterns**: [Ready/Not Ready]
- **Development Context**: [Prepared/Needs Attention]

## Recommendations

### For Immediate Development

- [Key standards to prioritize in current work]
- [Most important compliance areas to focus on]
- [Quick wins for following standards]

### For Architecture Maintenance

- [Suggestions for improving architecture documentation]
- [Missing standards that should be documented]
- [Opportunities for better cross-document consistency]
```

## Integration with Dev Workflow

### On Agent Activation

```
Automatically execute load-architecture-standards to:
- Discover all available architecture documents
- Load comprehensive development standards
- Prepare validation context for compliance checking
- Create development-ready standards reference
```

### Before Each Story Implementation

```
Reference loaded standards to:
- Understand applicable architectural constraints
- Choose appropriate implementation patterns
- Validate technology and approach decisions
- Ensure consistency with project standards
```

### During Implementation Validation

```
Use loaded standards for:
- Automated compliance checking with search patterns
- Symbol validation against approved technologies
- File organization compliance verification
- API and interface standard adherence
```

## Dynamic Architecture Benefits

### Comprehensive Coverage

- **No Missing Standards**: Automatically includes all architecture documents
- **Future-Proof**: New documents automatically included without config changes
- **Project-Specific**: Adapts to each project's unique architecture structure

### Maintenance Advantages

- **Self-Updating**: Reflects changes in architecture documentation
- **No Manual Config**: No need to update devLoadAlwaysFiles lists
- **Flexible Structure**: Works with any architecture document organization

### Development Efficiency

- **Complete Context**: Developers have access to all relevant standards
- **Consistent Application**: Same standards applied across all development
- **Validation Ready**: Prepares patterns for automated compliance checking

## Semantic Analysis Integration

### Document Discovery

```
Use list_dir and find_file to:
- Discover all architecture documents dynamically
- Handle nested directory structures
- Identify document types and purposes
```

### Content Analysis

```
Use search_for_pattern to:
- Extract standards and requirements from documents
- Identify compliance patterns and rules
- Cross-reference standards between documents
```

### Validation Preparation

```
Prepare patterns for validate-architecture-compliance:
- Coding standard validation patterns
- Technology usage compliance patterns
- Structural organization validation patterns
```

## Success Criteria

- All architecture documents discovered and loaded
- Standards consolidated into development-ready reference
- Validation patterns prepared for compliance checking
- Development context fully prepared for implementation
- Loading process adaptable to any project structure

## Notes

- Replaces static devLoadAlwaysFiles with dynamic discovery
- Scales automatically with project architecture documentation
- Integrates seamlessly with existing semantic validation
- Supports BMAD framework's sharded documentation approach
- Maintains backward compatibility with existing architecture structures

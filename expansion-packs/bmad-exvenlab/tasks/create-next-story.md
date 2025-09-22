<!-- Powered by BMAD™ Core -->

# Create Next Story Task

## Purpose

To identify the next logical story based on project progress and epic definitions, and then to prepare a comprehensive, self-contained, and actionable story file using the `Story Template`. This task ensures the story is enriched with all necessary technical context, requirements, and acceptance criteria, making it ready for efficient implementation by a Developer Agent with minimal need for additional research or finding its own context.

## SEQUENTIAL Task Execution (Do not proceed until current Task is complete)

### 0. Load Core Configuration and Check Workflow

- Load config.yaml using mcp**serena**find_symbol for configuration symbols
- If the file does not exist, HALT and inform the user: "config.yaml not found. This file is required for story creation. You can either: 1) Copy it from GITHUB bmad-core/config.yaml and configure it for your project OR 2) Run the BMad installer against your project to upgrade and add the file automatically. Please add and configure config.yaml before proceeding."
- Extract key configurations: `devStoryLocation`, `prd.*`, `architecture.*`, `workflow.*`

### 1. Identify Next Story for Preparation

#### 1.1 Locate Epic Files and Review Existing Stories

- Based on `prdSharded` from config, use mcp**serena**search_for_pattern to locate epic files (sharded location/pattern or monolithic PRD sections)
- If `devStoryLocation` has story files, use mcp**serena**get_symbols_overview to find the highest `{epicNum}.{storyNum}.story.md` file
- **If highest story exists:**
  - Verify status is 'Done'. If not, alert user: "ALERT: Found incomplete story! File: {lastEpicNum}.{lastStoryNum}.story.md Status: [current status] You should fix this story first, but would you like to accept risk & override to create the next story in draft?"
  - If proceeding, select next sequential story in the current epic
  - If epic is complete, prompt user: "Epic {epicNum} Complete: All stories in Epic {epicNum} have been completed. Would you like to: 1) Begin Epic {epicNum + 1} with story 1 2) Select a specific story to work on 3) Cancel story creation"
  - **CRITICAL**: NEVER automatically skip to another epic. User MUST explicitly instruct which story to create.
- **If no story files exist:** The next story is ALWAYS 1.1 (first story of first epic)
- Announce the identified story to the user: "Identified next story for preparation: {epicNum}.{storyNum} - {Story Title}"

### 2. Gather Story Requirements and Previous Story Context

- Extract story requirements from the identified epic file
- If previous story exists, review Dev Agent Record sections for:
  - Completion Notes and Debug Log References
  - Implementation deviations and technical decisions
  - Challenges encountered and lessons learned
- Extract relevant insights that inform the current story's preparation

### 3. Gather Architecture Context

#### 3.1 Determine Architecture Reading Strategy

- **If `architectureVersion: >= v4` and `architectureSharded: true`**: Read `{architectureShardedLocation}/index.md` then follow structured reading order below
- **Else**: Use monolithic `architectureFile` for similar sections

#### 3.2 Read Architecture Documents Based on Story Type

**Memory-First Architecture Reading:**
Use mcp**serena**read_memory to access architecture sections from Serena memory:

**For ALL Stories:**

- `mcp__serena__read_memory('architecture-tech-stack')` - Technology stack and frameworks
- `mcp__serena__read_memory('architecture-coding-standards')` - Development standards and patterns
- `mcp__serena__read_memory('architecture-project-structure')` - Project organization and conventions
- `mcp__serena__read_memory('architecture-testing-strategy')` - Testing approaches and requirements

**For Backend/API Stories, additionally:**

- `mcp__serena__read_memory('architecture-data-models')` - Data structures and relationships
- `mcp__serena__read_memory('architecture-database-schema')` - Database design and constraints
- `mcp__serena__read_memory('architecture-backend-design')` - Backend architecture patterns
- `mcp__serena__read_memory('architecture-api-specifications')` - API contracts and standards

**For Frontend/UI Stories, additionally:**

- `mcp__serena__read_memory('architecture-frontend-design')` - Frontend architecture and patterns
- `mcp__serena__read_memory('architecture-components')` - Component specifications and design
- `mcp__serena__read_memory('architecture-user-workflows')` - User interaction patterns

**For Full-Stack Stories:** Read both Backend and Frontend sections above using memory-based access

#### 3.3 Extract Story-Specific Technical Details

Extract ONLY information directly relevant to implementing the current story. Do NOT invent new libraries, patterns, or standards not in the source documents.

Extract:

- Specific data models, schemas, or structures the story will use
- API endpoints the story must implement or consume
- Component specifications for UI elements in the story
- File paths and naming conventions for new code
- Testing requirements specific to the story's features
- Security or performance considerations affecting the story

ALWAYS cite source documents: `[Source: architecture/{filename}.md#{section}]`

### 4. Verify Project Structure Alignment

- Cross-reference story requirements with Project Structure Guide from `docs/architecture/unified-project-structure.md`
- Ensure file paths, component locations, or module names align with defined structures
- Document any structural conflicts in "Project Structure Notes" section within the story draft

### 5. Populate Story Template with Full Context

- Create new story file: `{devStoryLocation}/{epicNum}.{storyNum}.story.md` using Story Template
- Fill in basic story information: Title, Status (Draft), Story statement, Acceptance Criteria from Epic
- **`Dev Notes` section (CRITICAL):**
  - CRITICAL: This section MUST contain ONLY information extracted from architecture documents. NEVER invent or assume technical details.
  - Include ALL relevant technical details from Steps 2-3, organized by category:
    - **Previous Story Insights**: Key learnings from previous story
    - **Data Models**: Specific schemas, validation rules, relationships [with source references]
    - **API Specifications**: Endpoint details, request/response formats, auth requirements [with source references]
    - **Component Specifications**: UI component details, props, state management [with source references]
    - **File Locations**: Exact paths where new code should be created based on project structure
    - **Testing Requirements**: Specific test cases or strategies from testing-strategy.md
    - **Technical Constraints**: Version requirements, performance considerations, security rules
  - Every technical detail MUST include its source reference: `[Source: architecture/{filename}.md#{section}]`
  - If information for a category is not found in the architecture docs, explicitly state: "No specific guidance found in architecture docs"
- **`Tasks / Subtasks` section:**
  - Generate detailed, sequential list of technical tasks based ONLY on: Epic Requirements, Story AC, Reviewed Architecture Information
  - Each task must reference relevant architecture documentation
  - Include unit testing as explicit subtasks based on the Testing Strategy
  - Link tasks to ACs where applicable (e.g., `Task 1 (AC: 1, 3)`)
- Add notes on project structure alignment or discrepancies found in Step 4

### 6. Story Draft Completion and Review

- Review all sections for completeness and accuracy
- Verify all source references are included for technical details
- Ensure tasks align with both epic requirements and architecture constraints
- Update status to "Draft" and save the story file
- Execute `{root}/tasks/execute-checklist` `{root}/checklists/story-draft-checklist`
- Provide summary to user including:
  - Story created: `{devStoryLocation}/{epicNum}.{storyNum}.story.md`
  - Status: Draft
  - Key technical components included from architecture docs
  - Any deviations or conflicts noted between epic and architecture
  - Checklist Results

## ✅ Story Creation Complete

**Story Created**: `{devStoryLocation}/{epicNum}.{storyNum}.story.md`
**Status**: Draft
**Epic Progress**: Story {storyNum} of Epic {epicNum}

### 🎯 What's Next?

**Development Workflow Options:**

**Option A: Begin Implementation (Recommended)**

```
@dev
*develop-story
```

Story is ready for development. Dev agent will implement all tasks and mark as "Review" when complete.

**Option B: Review Story First (Complex Stories)**

```
@po
Run task: validate-next-story
```

Optional validation for complex stories before development begins.

### 📊 Epic Status

Use mcp**serena**search_for_pattern to check remaining stories in Epic {epicNum}:

- **If more stories needed**: After dev completes this story, return to @sm for next story
- **If epic complete**: After dev completes this story, consider epic retrospective

### 🔄 Development Cycle

**Expected Flow:**

1. **Dev Implementation** → Story status: "Review"
2. **QA Review** (Optional) → Story status: "Done"
3. **Next Story** → Return to @sm \*draft OR Epic complete

---

**❓ Need guidance?** Run: `{root}/tasks/workflow-navigator.md` or ask "What should I do next?"

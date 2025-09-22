<!-- Powered by BMAD™ Core -->

# Workflow Navigator Task

## Purpose

Provides intelligent workflow orchestration by detecting current project state and recommending next steps. Solves the critical gap where users complete tasks but don't know what to do next to continue workflows.

## When to Use This Task

- **After completing any major task** when unsure of next steps
- **When starting a project** and need workflow guidance
- **When stuck between workflow phases**
- **When switching from Web UI to IDE** and need to understand current state
- **When resuming work** on an existing project

## Task Instructions

### Step 1: Project Context Discovery

Use Serena tools to analyze current project state:

```yaml
context_analysis:
  - Use mcp__serena__list_dir with recursive=true to examine docs/ structure
  - Use mcp__serena__search_for_pattern to find existing artifacts (prd.md, architecture.md, stories/, etc.)
  - Use mcp__serena__get_symbols_overview for key documents to understand completion status
  - Check for workflow indicators in config.yaml or project structure
```

### Step 2: Workflow State Detection

Based on discovered artifacts, determine:

#### A. Project Type Classification

```yaml
greenfield_indicators:
  - docs/ contains: project-brief.md, prd.md, front-end-spec.md, fullstack-architecture.md
  - No existing codebase or legacy system references
  - Documentation follows greenfield templates

brownfield_indicators:
  - docs/ contains: brownfield-architecture.md, existing system analysis
  - References to existing codebase, technical debt, integration points
  - Documentation follows brownfield templates

single_task_indicators:
  - Single story file in docs/stories/
  - No comprehensive PRD or architecture docs
  - Focused enhancement scope
```

#### B. Workflow Phase Detection

```yaml
planning_phase:
  indicators: [project-brief.md exists, prd.md missing or incomplete]
  next_steps: 'Continue with PM agent for PRD creation'

architecture_phase:
  indicators: [prd.md exists, architecture docs missing]
  next_steps: 'Continue with Architect agent for system design'

validation_phase:
  indicators: [All docs exist, no validation checklist results]
  next_steps: 'Continue with PO agent for document validation'

sharding_phase:
  indicators: [Monolithic docs exist, no docs/prd/ or docs/architecture/ folders]
  next_steps: 'Continue with PO agent for document sharding'

development_phase:
  indicators: [Sharded docs exist, stories/ folder missing or incomplete]
  next_steps: 'Continue with SM agent for story creation'

implementation_phase:
  indicators: [Stories exist in Draft/Approved status]
  next_steps: 'Continue with Dev agent for implementation'

review_phase:
  indicators: [Stories in Review status, no QA results]
  next_steps: 'Continue with QA agent for code review'

completion_phase:
  indicators: [All stories Done, no retrospective]
  next_steps: 'Optional: PO agent for epic retrospective'
```

### Step 3: Generate Contextual Recommendations

Based on detected state, provide:

#### A. Current Status Summary

```markdown
## Current Project Status

**Project Type**: {{greenfield|brownfield|single-task}}
**Workflow**: {{workflow_name}}
**Current Phase**: {{phase_name}}
**Progress**: {{completion_percentage}}%

**Artifacts Found**:

- ✅ {{existing_artifacts}}
- ❌ {{missing_artifacts}}

**Current Story Status** (if applicable):

- {{story_count}} stories total
- {{draft_count}} in Draft
- {{approved_count}} in Approved
- {{review_count}} in Review
- {{done_count}} Done
```

#### B. Next Step Recommendations

**Primary Next Action:**

```markdown
### 🎯 Recommended Next Step

**Action**: {{action_description}}
**Agent**: {{agent_name}}
**Command**: {{exact_command_to_run}}
**Context**: {{why_this_is_next}}

**Example**:
```

@sm
\*draft

```

**Expected Outcome**: {{what_will_be_created}}
```

**Alternative Actions:**

```markdown
### 🔄 Alternative Options

1. **{{alternative_1}}**: {{description_and_command}}
2. **{{alternative_2}}**: {{description_and_command}}
3. **{{alternative_3}}**: {{description_and_command}}
```

### Step 4: Workflow Transition Guidance

Provide ready-to-use transition prompts:

#### A. Agent Handoff Prompts

```markdown
### 📋 Ready-to-Use Prompts

**For {{next_agent}}:**
```

{{handoff_prompt_from_workflow_yaml}}

```

**For User:**
```

{{user_action_required}}

```

```

#### B. File Management Instructions

```markdown
### 📁 File Management

**Save/Copy Required**:

- {{file_1}} → {{destination_1}}
- {{file_2}} → {{destination_2}}

**Verify Structure**:

- {{folder_structure_requirements}}
```

### Step 5: Workflow Progress Tracking

Use Serena memory to track progress:

```yaml
progress_tracking:
  - Use mcp__serena__write_memory to store workflow state
  - Memory key: 'workflow-progress-{{project_name}}'
  - Include: current_phase, completed_tasks, next_actions
  - Update on each workflow navigator run
```

## Success Criteria

- **Clear Status**: User understands exactly where they are in the workflow
- **Actionable Next Steps**: Specific commands and agents to use next
- **Context Preservation**: No lost progress or repeated work
- **Smooth Transitions**: Seamless handoffs between agents and phases
- **Progress Visibility**: Clear understanding of overall workflow completion

## Special Cases

### Case 1: Web UI to IDE Transition

```markdown
**Detected**: Comprehensive docs in docs/ folder but no IDE development started
**Guidance**: "Ready for IDE development phase. Start with document sharding."
**Next Action**: "@po → shard docs/prd.md"
```

### Case 2: Resume Interrupted Development

```markdown
**Detected**: Stories exist, some in various states
**Guidance**: "Development in progress. Resume with incomplete stories."
**Next Action**: "@dev → continue with story {{story_id}}"
```

### Case 3: Workflow Complete

```markdown
**Detected**: All stories Done, all artifacts validated
**Guidance**: "🎉 Workflow complete! All development finished."
**Optional**: "Run retrospective for learnings documentation"
```

## Integration with Other Tasks

Other tasks can call this workflow navigator by including:

```markdown
## Workflow Navigation

For next steps after completing this task, run:
`workflow-navigator.md` or ask: "What should I do next?"

Current task completed: {{task_name}}
Expected next phase: {{expected_next_phase}}
```

## Configuration Integration

Add to config.yaml:

```yaml
workflow_tracking:
  enabled: true
  auto_navigate: true
  progress_memory: true
  transition_prompts: true
```

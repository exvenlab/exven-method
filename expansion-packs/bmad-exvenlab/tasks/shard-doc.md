<!-- Powered by BMAD™ Core -->

# Document Sharding Task

## Purpose

- Split a large document into multiple smaller documents based on level 2 sections
- Create a folder structure to organize the sharded documents
- Maintain all content integrity including code blocks, diagrams, and markdown formatting

## Primary Method: Serena Memory Storage

[[LLM: First, check if architecture_storage.mode is set to "memory" in {root}/config.yaml. If it is, proceed with Serena memory sharding method below.

If architecture_storage.mode is not set or set to "files", check if markdownExploder is set to true. If markdownExploder is true, attempt to run the command: `md-tree explode {input file} {output path}`.

If the command succeeds, inform the user that the document has been sharded successfully and STOP - do not proceed further.

If the command fails (especially with an error indicating the command is not found or not available), inform the user: "The markdownExploder setting is enabled but the md-tree command is not available. Please either:

1. Install @kayvan/markdown-tree-parser globally with: `npm install -g @kayvan/markdown-tree-parser`
2. Or set markdownExploder to false in {root}/config.yaml

**IMPORTANT: STOP HERE - do not proceed with manual sharding until one of the above actions is taken.**"

If markdownExploder is set to false, inform the user: "The markdownExploder setting is currently false. For better performance and reliability, you should:

1. Set markdownExploder to true in {root}/config.yaml
2. Install @kayvan/markdown-tree-parser globally with: `npm install -g @kayvan/markdown-tree-parser`

I will now proceed with the manual sharding process."

Then proceed with the manual method below ONLY if markdownExploder is false.]]

## Serena Memory Sharding Method

When `architecture_storage.mode: "memory"` in config.yaml, use this method:

### Step 1: Parse Source Document

1. **Read the source document** using mcp**serena**find_symbol to get full content
2. **Identify level 2 sections** (## headings) as logical boundaries
3. **Extract each section** with complete content including subsections

### Step 2: Store Sections in Serena Memory

For each extracted section:

```yaml
memory_storage_process:
  parse_section:
    - 'Extract section heading and full content'
    - 'Include all subsections, code blocks, diagrams'
    - 'Preserve complete markdown formatting'

  create_memory_key:
    - 'Convert heading to memory key format'
    - "Example: '## Tech Stack' → 'architecture-tech-stack'"
    - "Example: '## Data Models' → 'architecture-data-models'"

  store_in_memory:
    - 'Use mcp__serena__write_memory with section content'
    - 'Include metadata: source_file, section_title, last_updated'
```

### Step 3: Create Memory Index

Store a master index in memory for navigation:

```yaml
memory_index_creation:
  key: 'architecture-index'
  content: |
    # Architecture Sections Index

    Source: {source_file_path}
    Last Updated: {timestamp}
    Sections: {section_count}

    ## Available Sections
    - architecture-tech-stack: "Tech Stack"
    - architecture-data-models: "Data Models"
    - architecture-backend-design: "Backend Design"
    - architecture-frontend-design: "Frontend Design"
    - architecture-database-schema: "Database Schema"
    - architecture-api-specifications: "API Specifications"

    ## Usage
    Read sections with: mcp__serena__read_memory('architecture-{section}')
```

### Step 4: Memory Storage Execution

Execute the memory storage process:

1. **For each section identified**:

   ```
   mcp__serena__write_memory(
     memory_name: "architecture-{section-slug}",
     content: {section_content_with_metadata}
   )
   ```

2. **Create navigation index**:

   ```
   mcp__serena__write_memory(
     memory_name: "architecture-index",
     content: {index_content}
   )
   ```

3. **Store source reference**:
   ```
   mcp__serena__write_memory(
     memory_name: "architecture-source",
     content: {source_file_info_and_timestamp}
   )
   ```

### Step 5: Validation and Reporting

After memory storage:

1. **Verify storage**: Use mcp**serena**read_memory to confirm all sections stored
2. **Report success**: Provide memory storage summary
3. **Update config**: Confirm memory mode is active

### Memory Storage Report Format

```markdown
## ✅ Architecture Stored in Serena Memory

**Source**: {source_document_path}
**Storage Mode**: Memory (Single Source of Truth)
**Sections Stored**: {section_count}

### Memory Keys Created:

- `architecture-index` - Navigation and overview
- `architecture-tech-stack` - Technology stack details
- `architecture-data-models` - Data models and schemas
- `architecture-backend-design` - Backend architecture
- `architecture-frontend-design` - Frontend architecture
- `architecture-database-schema` - Database design
- `architecture-api-specifications` - API documentation

### Usage for Agents:
```

# Read specific section

mcp**serena**read_memory('architecture-tech-stack')

# Get full index

mcp**serena**read_memory('architecture-index')

```

### Benefits:
- ✅ Single source of truth: {source_document}
- ✅ No file proliferation in docs/architecture/
- ✅ Dynamic access via Serena tools
- ✅ Memory persistence across sessions
```

---

### Installation and Usage

1. **Install globally**:

   ```bash
   npm install -g @kayvan/markdown-tree-parser
   ```

2. **Use the explode command**:

   ```bash
   # For PRD
   md-tree explode docs/prd.md docs/prd

   # For Architecture
   md-tree explode docs/architecture.md docs/architecture

   # For any document
   md-tree explode [source-document] [destination-folder]
   ```

3. **What it does**:
   - Automatically splits the document by level 2 sections
   - Creates properly named files
   - Adjusts heading levels appropriately
   - Handles all edge cases with code blocks and special markdown

If the user has @kayvan/markdown-tree-parser installed, use it and skip the manual process below.

---

## Manual Method (if @kayvan/markdown-tree-parser is not available or user indicated manual method)

### Task Instructions

1. Identify Document and Target Location

- Determine which document to shard (user-provided path)
- Create a new folder under `docs/` with the same name as the document (without extension)
- Example: `docs/prd.md` → create folder `docs/prd/`

2. Parse and Extract Sections

CRITICAL AEGNT SHARDING RULES:

1. Read the entire document content
2. Identify all level 2 sections (## headings)
3. For each level 2 section:
   - Extract the section heading and ALL content until the next level 2 section
   - Include all subsections, code blocks, diagrams, lists, tables, etc.
   - Be extremely careful with:
     - Fenced code blocks (```) - ensure you capture the full block including closing backticks and account for potential misleading level 2's that are actually part of a fenced section example
     - Mermaid diagrams - preserve the complete diagram syntax
     - Nested markdown elements
     - Multi-line content that might contain ## inside code blocks

CRITICAL: Use proper parsing that understands markdown context. A ## inside a code block is NOT a section header.]]

### 3. Create Individual Files

For each extracted section:

1. **Generate filename**: Convert the section heading to lowercase-dash-case
   - Remove special characters
   - Replace spaces with dashes
   - Example: "## Tech Stack" → `tech-stack.md`

2. **Adjust heading levels**:
   - The level 2 heading becomes level 1 (# instead of ##) in the sharded new document
   - All subsection levels decrease by 1:

   ```txt
     - ### → ##
     - #### → ###
     - ##### → ####
     - etc.
   ```

3. **Write content**: Save the adjusted content to the new file

### 4. Create Index File

Create an `index.md` file in the sharded folder that:

1. Contains the original level 1 heading and any content before the first level 2 section
2. Lists all the sharded files with links:

```markdown
# Original Document Title

[Original introduction content if any]

## Sections

- [Section Name 1](./section-name-1.md)
- [Section Name 2](./section-name-2.md)
- [Section Name 3](./section-name-3.md)
  ...
```

### 5. Preserve Special Content

1. **Code blocks**: Must capture complete blocks including:

   ```language
   content
   ```

2. **Mermaid diagrams**: Preserve complete syntax:

   ```mermaid
   graph TD
   ...
   ```

3. **Tables**: Maintain proper markdown table formatting

4. **Lists**: Preserve indentation and nesting

5. **Inline code**: Preserve backticks

6. **Links and references**: Keep all markdown links intact

7. **Template markup**: If documents contain {{placeholders}} ,preserve exactly

### 6. Validation

After sharding:

1. Verify all sections were extracted
2. Check that no content was lost
3. Ensure heading levels were properly adjusted
4. Confirm all files were created successfully

### 7. Report Results

Provide a summary:

```text
Document sharded successfully:
- Source: [original document path]
- Destination: docs/[folder-name]/
- Files created: [count]
- Sections:
  - section-name-1.md: "Section Title 1"
  - section-name-2.md: "Section Title 2"
  ...
```

## Important Notes

- Never modify the actual content, only adjust heading levels
- Preserve ALL formatting, including whitespace where significant
- Handle edge cases like sections with code blocks containing ## symbols
- Ensure the sharding is reversible (could reconstruct the original from shards)

# Memory-Based Architecture Workflow

## Overview

BMAD-ExvenLab now supports **Serena Memory-based Architecture Storage** as the default for new projects with Serena users. This eliminates file proliferation while maintaining single source of truth architecture.

## Configuration

### Enable Memory Mode

In `config.yaml`:

```yaml
# Architecture storage configuration
architecture_storage:
  mode: 'memory'
  memory_prefix: 'architecture-'
  source_file: 'docs/architecture.md'
  single_source_of_truth: true
```

## Memory Architecture Workflow

### 1. Create Architecture Document

**Standard process** - create `docs/architecture.md` using architect agent:

```
@architect
*create-full-stack-architecture
```

**Result**: Single monolithic `docs/architecture.md` file

### 2. Shard to Memory

**Instead of creating files**, store sections in Serena memory:

```
@po
*shard-doc docs/architecture.md
```

**Process**:

- Parses `docs/architecture.md` sections
- Stores each section in Serena memory with structured keys
- Creates navigation index in memory
- **No files created** in `docs/architecture/`

### 3. Memory Structure Created

**Memory Keys**:

```
architecture-index          # Navigation and section list
architecture-tech-stack     # Technology stack details
architecture-data-models    # Data models and schemas
architecture-backend-design # Backend architecture
architecture-frontend-design# Frontend architecture
architecture-database-schema# Database design
architecture-api-specifications # API documentation
```

### 4. Story Creation with Memory

**Stories read from memory** instead of files:

```
@sm
*draft
```

**Process**:

- Uses `mcp__serena__read_memory('architecture-tech-stack')` instead of file reading
- Gets targeted architecture context for story
- Single source of truth maintained

## Benefits

### ✅ Single Source of Truth

- **docs/architecture.md** remains authoritative
- No file sync issues
- Updates reflect immediately
- Clean project structure

### ✅ Serena Integration

- Native memory persistence
- Cross-session architecture context
- Workflow state tracking
- Memory-based navigation

### ✅ Developer Experience

- No docs/architecture/ folder clutter
- Faster context loading via memory
- Dynamic architecture access
- Workflow continuity

## Memory Commands

### Read Architecture Sections

```bash
# Get section index
mcp__serena__read_memory('architecture-index')

# Read specific sections
mcp__serena__read_memory('architecture-tech-stack')
mcp__serena__read_memory('architecture-data-models')
mcp__serena__read_memory('architecture-backend-design')
```

### Update Architecture

1. **Edit source**: Update `docs/architecture.md`
2. **Re-shard**: Run `@po *shard-doc docs/architecture.md`
3. **Memory updated**: All sections refresh automatically

## Workflow Navigation

### Check Architecture Status

```
@any-agent
*workflow
```

**Detection**:

- Checks for `architecture-index` in memory
- Identifies memory-based vs file-based architecture
- Provides appropriate guidance

### Memory vs Files

**Memory Mode** (Default for Serena users):

- Source: `docs/architecture.md`
- Storage: `.serena/memories/`
- Access: `mcp__serena__read_memory()`

**File Mode** (Legacy/Non-Serena):

- Source: `docs/architecture.md`
- Storage: `docs/architecture/*.md`
- Access: File reading

## Best Practices

### 1. Keep Source Updated

- Always edit `docs/architecture.md` (never memory directly)
- Re-shard after significant changes
- Use version control for source file

### 2. Memory Hygiene

- Use workflow navigator to check memory status
- Re-shard if memory seems stale
- Trust memory over files in memory mode

### 3. Team Coordination

- All team members use Serena
- Consistent memory mode across team
- Share `docs/architecture.md` via git

## Troubleshooting

### Memory Not Found

**Problem**: `mcp__serena__read_memory('architecture-index')` returns empty

**Solution**:

```
@po
*shard-doc docs/architecture.md
```

### Stale Memory

**Problem**: Memory content doesn't match `docs/architecture.md`

**Solution**:

1. Verify `docs/architecture.md` is current
2. Re-shard: `@po *shard-doc docs/architecture.md`
3. Confirm memory updated

### Mixed Mode Issues

**Problem**: Some agents read files, others read memory

**Solution**:

1. Check `config.yaml` has `architecture_storage.mode: "memory"`
2. Ensure all agents updated to memory mode
3. Remove old `docs/architecture/` files to avoid confusion

## Migration from File Mode

### Existing Projects

If you have existing `docs/architecture/*.md` files:

1. **Consolidate to source**:

   ```bash
   # Manually merge all files back to docs/architecture.md
   ```

2. **Switch to memory mode**:

   ```yaml
   # config.yaml
   architecture_storage:
     mode: 'memory'
   ```

3. **Shard to memory**:

   ```
   @po
   *shard-doc docs/architecture.md
   ```

4. **Remove old files**:
   ```bash
   rm -rf docs/architecture/
   ```

## Summary

**Memory-based architecture storage** provides:

- ✅ Single source of truth
- ✅ No file proliferation
- ✅ Serena-native workflow
- ✅ Dynamic architecture access
- ✅ Cleaner project structure

**Perfect for**: New projects with Serena-native teams seeking optimal architecture management.

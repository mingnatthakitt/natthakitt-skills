---
name: wiki
description: Analyze the repository and generate a structured Wiki with architecture overviews, module breakdowns, API documentation, and cross-linked pages. Trigger on /wiki or when the user asks to generate documentation, create a wiki, or document the codebase.
---

# Wiki — Auto-Generated Codebase Documentation

Generates a comprehensive, structured Wiki for the repository by analyzing code structure and producing browsable markdown and HTML documentation with interactive mindmaps.

**IMPORTANT:** When this skill is invoked, you MUST:
1. Analyze the codebase thoroughly
2. Create actual files in the project directory using Write tool
3. Generate BOTH markdown AND HTML outputs with mindmap

## Trigger Conditions

- User invokes `/wiki`
- User asks to "generate documentation", "create wiki", "document the codebase"
- User requests a "codebase overview", "architecture docs", or "project documentation"

## Wiki Structure

### Markdown Output (`{project-root}/.claude/wiki/`)

```
.claude/wiki/
├── README.md                    # Entry point — overview and navigation
├── architecture.md              # High-level architecture and design decisions
├── modules/
│   ├── index.md                 # Module overview
│   ├── [module-name].md        # Per-module documentation
├── api/
│   ├── index.md                 # API overview
│   ├── [api-name].md           # Per-API endpoint documentation
├── patterns.md                  # Common patterns and conventions
└── resources.md                 # External resources, configs, env vars
```

### HTML Output (`{project-root}/.claude/wiki/html/`)

```
.claude/wiki/html/
├── index.html                   # Main wiki page with navigation
├── mindmap.html                 # Interactive architecture mindmap
├── styles.css                   # Wiki styling
└── assets/
    └── mindmap-data.json        # Mindmap structure data
```

## Generation Process

### Phase 1: Analyze the Codebase

Read and analyze (use Bash `ls` and Read tool):
- Source files (`.ts`, `.js`, `.py`, `.go`, `.rs`, etc.)
- Configuration files (`package.json`, `pyproject.toml`, `Cargo.toml`, etc.)
- Test files to understand expected behavior
- README and existing documentation
- Entry points and main modules
- Build scripts, CI/CD pipelines, task runners

Build a mental map of:
- Project structure and directory layout
- Main modules and their responsibilities
- Public APIs and their signatures
- Configuration and environment variables
- Patterns and conventions used
- Workflows (build, test, deploy, CI/CD)
- Data flow between components

### Phase 2: Create Directory Structure

First, create the required directories:

```bash
mkdir -p .claude/wiki/modules
mkdir -p .claude/wiki/api
mkdir -p .claude/wiki/html/assets
mkdir -p .claude/wiki/figures
```

### Phase 3: Generate and Write All Files

Use the Write tool to create EVERY file. Do NOT just describe what would be created — actually create the files.

#### Required Markdown Files:
1. `.claude/wiki/README.md` — Entry point with overview and navigation
2. `.claude/wiki/architecture.md` — High-level architecture
3. `.claude/wiki/modules/index.md` — Module overview
4. `.claude/wiki/modules/[module-name].md` — Per-module docs
5. `.claude/wiki/api/index.md` — API overview
6. `.claude/wiki/api/[api-name].md` — Per-API docs
7. `.claude/wiki/patterns.md` — Patterns and conventions
8. `.claude/wiki/resources.md` — Configs and env vars

#### Required HTML Files:
1. `.claude/wiki/html/index.html` — Main web wiki
2. `.claude/wiki/html/mindmap.html` — Interactive mindmap
3. `.claude/wiki/html/styles.css` — Styling
4. `.claude/wiki/html/assets/mindmap-data.json` — Mindmap data

### File Generation Details

#### README.md (Entry Point)
```markdown
# {Project Name} Wiki

Generated on {date}

## Overview
Brief description of what this project does.

## Quick Navigation
- [Architecture](architecture.md)
- [Modules](modules/)
- [API](api/)
- [Patterns](patterns.md)
- [Resources](resources.md)
- [HTML Version](./html/index.html) — Interactive web version
- [Mind Map](./html/mindmap.html) — Visual architecture

## Statistics
- Total modules: N
- API endpoints: N
- Main patterns: ...
```

#### architecture.md
- High-level system design
- Component relationships
- Data flow
- Key design decisions and their rationale

#### modules/index.md + [module-name].md
- Module purpose and responsibilities
- Public interfaces
- Dependencies on other modules
- Key classes/functions

#### api/index.md + [api-name].md
- Endpoint definitions
- Request/response shapes
- Authentication requirements
- Error handling patterns

#### patterns.md
- Coding conventions used
- Common patterns (DI, events, state management, etc.)
- Style guidelines
- Naming conventions

#### resources.md
- Environment variables
- Configuration options
- External service dependencies
- Deployment notes

### HTML Implementation

#### index.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{Project Name} Wiki</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <nav class="sidebar">
        <h1>{Project Name}</h1>
        <ul>
            <li><a href="index.html">Overview</a></li>
            <li><a href="mindmap.html">Architecture Mind Map</a></li>
        </ul>
    </nav>
    <main>
        <!-- generated content -->
    </main>
</body>
</html>
```

#### mindmap.html
Use Markmap for simple integration:
```html
<script src="https://cdn.jsdelivr.net/npm/markmap-autoloader"></script>
```

Or D3.js for custom interactive mindmap with:
- Zoom and pan controls
- Click to expand/collapse nodes
- Hover tooltips with module details

#### styles.css
Modern, clean styling with sidebar navigation, responsive layout, syntax highlighting.

### Mindmap Data Structure

Generate `mindmap-data.json`:
```json
{
  "name": "{Project Name}",
  "children": [
    {
      "name": "Architecture",
      "children": [
        { "name": "Core", "children": [] },
        { "name": "Data Layer", "children": [] }
      ]
    },
    {
      "name": "Workflows",
      "children": [
        { "name": "Build", "children": [] },
        { "name": "Test", "children": [] },
        { "name": "Deploy", "children": [] }
      ]
    },
    {
      "name": "API",
      "children": [
        { "name": "/users", "children": [] },
        { "name": "/data", "children": [] }
      ]
    }
  ]
}
```

## Configuration

### Output Location
- Markdown: `{project-root}/.claude/wiki/`
- HTML: `{project-root}/.claude/wiki/html/`

### Options
- `--force` — overwrite existing wiki
- `--modules-only` — only generate module docs (skip API)
- `--html-only` — skip markdown, only generate HTML
- `--mindmap-only` — only generate mindmap visualization

## Quality Standards

- Every module must have a documentation page
- Every public API must be documented with request/response examples
- Cross-references must be accurate and functional
- Code examples must be runnable and up-to-date
- HTML must be responsive and work on mobile
- Mindmap must be interactive with zoom/pan support

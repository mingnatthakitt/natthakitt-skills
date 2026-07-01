# Claude Code Agent Skills

A collection of custom skills for [Claude Code](https://claude.ai/code) that extend its capabilities for codebase documentation, research, and analysis.

## Skills

### Wiki (`wiki`)
Generates a comprehensive **dark-themed HTML manual** ("The Holy Grail") with embedded SVG diagrams, plus structured markdown documentation for repositories.

**Trigger:** `/wiki`

**Features:**
- Full codebase analysis — every module, function, API endpoint, and pattern
- **SVG mindmap** — hierarchical architecture tree with color-coded branches
- **SVG architecture diagram** — component-level system design with data-flow arrows
- **SVG workflow diagram** — CI/CD pipeline: Build → Test → Deploy → Monitor stages
- **Dark-themed HTML manual** — single-page `index.html` with all SVGs embedded inline, sidebar nav, no external dependencies
- Markdown docs: README, architecture, modules, API, patterns, resources (redacted), workflows
- Security-first: all `.env`, secrets, API keys, and credentials are redacted
- All SVGs use right-angle connectors, grid-based layout, and minimum 14px fonts to prevent overlapping text

**Usage:**
```bash
/wiki                  # Generate full wiki (markdown + HTML manual)
/wiki --force          # Overwrite existing wiki
/wiki --modules-only   # Only generate module docs
/wiki --api-only       # Only generate API docs
/wiki --html-only      # Skip markdown, only generate HTML manual
/wiki --mindmap-only   # Only generate the SVG mindmap
```

---

### Manuscript (`manuscript`)
Produces academically-formatted research manuscripts with LaTeX equations, BibTeX citations, and publication-ready structure.

**Trigger:** `/manuscript`

**Features:**
- Deep codebase exploration and analysis
- Cross-references with existing wiki documentation
- LaTeX mathematical formalization of algorithms
- Academic citations (BibTeX format)
- Generated figures (architecture, data flow, state machines)
- Complete LaTeX document with proper section structure

**Usage:**
```bash
/manuscript
/manuscript --depth=deep --equations=true --citations=true
```

---

## Installation

### Option 1: npx skills add (Recommended)

Install using the [skills CLI](https://github.com/vercel-labs/skills) by Vercel Labs:

```bash
# Install all skills
npx skills add mingnatthakitt/natthakitt-skills

# Install specific skills only
npx skills add mingnatthakitt/natthakitt-skills --skill wiki
npx skills add mingnatthakitt/natthakitt-skills --skill manuscript

# Install globally (available to all projects)
npx skills add mingnatthakitt/natthakitt-skills --global

# Install with confirmation skipped
npx skills add mingnatthakitt/natthakitt-skills --yes
```

---

### Option 2: Git Clone + Symlink

```bash
# Clone the repository
git clone https://github.com/mingnatthakitt/natthakitt-skills.git ~/natthakitt-skills

# Create symlinks
mkdir -p ~/.claude/skills
ln -s ~/natthakitt-skills/skills/wiki ~/.claude/skills/wiki
ln -s ~/natthakitt-skills/skills/manuscript ~/.claude/skills/manuscript
```

---

### Option 3: Per-Project Installation

```bash
# In your project directory
git clone https://github.com/mingnatthakitt/natthakitt-skills.git .claude/natthakitt-skills

# Create symlinks
mkdir -p .claude/skills
ln -s .claude/natthakitt-skills/skills/wiki .claude/skills/wiki
ln -s .claude/natthakitt-skills/skills/manuscript .claude/skills/manuscript
```

---

### Option 4: Direct Copy

```bash
# Clone anywhere
git clone https://github.com/mingnatthakitt/natthakitt-skills.git /path/to/natthakitt-skills

# Copy directly to skills directory
cp -r /path/to/natthakitt-skills/skills/wiki ~/.claude/skills/wiki
cp -r /path/to/natthakitt-skills/skills/manuscript ~/.claude/skills/manuscript
```

---

## Quick Start

```bash
# One-liner installation
npx skills add mingnatthakitt/natthakitt-skills --yes

# Use in Claude Code
/wiki        # Generate documentation
/manuscript  # Generate research paper
```

---

## Structure

```
natthakitt-skills/
├── README.md
└── skills/
    ├── wiki/
    │   └── SKILL.md           # Wiki skill definition
    └── manuscript/
        └── SKILL.md           # Manuscript skill definition
```

---

## Skill Format

Each skill is a directory containing `SKILL.md` with YAML frontmatter:

```markdown
---
name: skill-name
description: What this skill does and when to trigger it
---

# Skill Title

Detailed instructions...
```

---

## Requirements

- [Claude Code](https://claude.ai/code) installed
- Node.js 18+ (for npx skills CLI)
- Git for cloning
- For Manuscript: LaTeX distribution (pdflatex, bibtex)

---

## License

MIT

---

## Links

- [Claude Code](https://claude.ai/code)
- [skills CLI by Vercel Labs](https://github.com/vercel-labs/skills)
- [natthakitt-skills GitHub](https://github.com/mingnatthakitt/natthakitt-skills)

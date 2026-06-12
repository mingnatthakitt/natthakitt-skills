# Claude Code Agent Skills

A collection of custom skills for [Claude Code](https://claude.ai/code) that extend its capabilities for codebase documentation, research, and analysis.

## Skills

### Wiki (`wiki`)
Generates comprehensive structured documentation for repositories with markdown pages and interactive HTML mindmaps.

**Trigger:** `/wiki`

**Features:**
- Analyzes codebase structure and architecture
- Generates markdown documentation (README, architecture, modules, API, patterns)
- Creates interactive HTML wiki with sidebar navigation
- Produces visual mindmaps for architecture and workflows
- Supports build, test, deploy, and CI/CD workflow visualization

**Usage:**
```bash
/wiki
/wiki --force          # Overwrite existing wiki
/wiki --deep           # More thorough analysis
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
npx skills add mingnatthakitt/ming-skills

# Install specific skills only
npx skills add mingnatthakitt/ming-skills --skill wiki
npx skills add mingnatthakitt/ming-skills --skill manuscript

# Install globally (available to all projects)
npx skills add mingnatthakitt/ming-skills --global

# Install with confirmation skipped
npx skills add mingnatthakitt/ming-skills --yes
```

---

### Option 2: Git Clone + Symlink

```bash
# Clone the repository
git clone https://github.com/mingnatthakitt/ming-skills.git ~/ming-skills

# Create symlinks
mkdir -p ~/.claude/skills
ln -s ~/ming-skills/skills/wiki ~/.claude/skills/wiki
ln -s ~/ming-skills/skills/manuscript ~/.claude/skills/manuscript
```

---

### Option 3: Per-Project Installation

```bash
# In your project directory
git clone https://github.com/mingnatthakitt/ming-skills.git .claude/ming-skills

# Create symlinks
mkdir -p .claude/skills
ln -s .claude/ming-skills/skills/wiki .claude/skills/wiki
ln -s .claude/ming-skills/skills/manuscript .claude/skills/manuscript
```

---

### Option 4: Direct Copy

```bash
# Clone anywhere
git clone https://github.com/mingnatthakitt/ming-skills.git /path/to/ming-skills

# Copy directly to skills directory
cp -r /path/to/ming-skills/skills/wiki ~/.claude/skills/wiki
cp -r /path/to/ming-skills/skills/manuscript ~/.claude/skills/manuscript
```

---

## Quick Start

```bash
# One-liner installation
npx skills add mingnatthakitt/ming-skills --yes

# Use in Claude Code
/wiki        # Generate documentation
/manuscript  # Generate research paper
```

---

## Structure

```
ming-skills/
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
- [ming-skills GitHub](https://github.com/mingnatthakitt/ming-skills)
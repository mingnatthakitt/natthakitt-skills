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

### Option 1: Manual Installation (Recommended)

Create symlinks to the skills directory:

```bash
# Create skills directory in your project
mkdir -p .claude/skills

# Link wiki skill
ln -s ~/Documents/CS/ming-skills/wiki ~/.claude/skills/wiki

# Link manuscript skill
ln -s ~/Documents/CS/ming-skills/manuscript ~/.claude/skills/manuscript
```

### Option 2: Clone and Link

```bash
# Clone this repository
git clone https://github.com/yourusername/ming-skills.git ~/Documents/CS/ming-skills

# Create symlinks in your project
ln -s ~/Documents/CS/ming-skills/wiki /path/to/project/.claude/skills/wiki
ln -s ~/Documents/CS/ming-skills/manuscript /path/to/project/.claude/skills/manuscript
```

### Option 3: Using claude-skills CLI

Use the [@spardutti/claude-skills](https://www.npmjs.com/package/@spardutti/claude-skills) interactive installer:

```bash
npx @spardutti/claude-skills
```

Then select the skills you want to install from the catalog.

---

## Structure

```
ming-skills/
├── README.md              # This file
├── wiki/
│   └── SKILL.md           # Wiki skill definition
└── manuscript/
    └── SKILL.md           # Manuscript skill definition
```

---

## Skill Format

Each skill is a directory containing:

- **`SKILL.md`** — The skill definition with:
  - YAML frontmatter (`name`, `description`, `trigger conditions`)
  - Markdown body with instructions and guidelines

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
- Node.js 18+ (for some CLI features)

---

## License

MIT

---

## Contributing

Contributions welcome! To add a new skill:

1. Create a directory under `skills/<skill-name>/`
2. Add a `SKILL.md` file with proper frontmatter
3. Follow the skill authoring conventions
4. Submit a pull request

---

## Links

- [Claude Code Documentation](https://docs.claude.com/claude-code)
- [@spardutti/claude-skills](https://www.npmjs.com/package/@spardutti/claude-skills) - Interactive skill installer
- [Awesome Claude Code Skills](https://github.com/topics/claude-code-skills) - Community skill collection

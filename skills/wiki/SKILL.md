---
name: wiki
description: Analyze the repository and generate a structured Wiki with architecture overviews, module breakdowns, API documentation, and cross-linked pages. Trigger on /wiki or when the user asks to generate documentation, create a wiki, or document the codebase.
---

# Wiki — Auto-Generated Codebase Documentation

Generates a comprehensive, structured Wiki for the repository by analyzing code structure and producing browsable markdown and a dark-themed HTML manual with embedded SVG mindmaps, architecture diagrams, and workflow visualizations.

**IMPORTANT:** When this skill is invoked, you MUST:
1. Analyze the codebase thoroughly — EVERYTHING including internal details
2. Create actual files in the project directory using Write tool
3. Generate BOTH markdown AND HTML outputs
4. Generate SVG mindmaps, architecture diagrams, and workflow visualizations
5. NEVER expose `.env` files, secrets, API keys, or sensitive configuration values

## Trigger Conditions

- User invokes `/wiki`
- User asks to "generate documentation", "create wiki", "document the codebase"
- User requests a "codebase overview", "architecture docs", or "project documentation"

## SECURITY — Never Expose These

**ALWAYS REDACT IN WIKI:**
- `.env` files and environment variables
- API keys, tokens, secrets
- Passwords and credentials
- Database connection strings
- Private keys and certificates
- Any file matching `.env*`, `.gitignore`, `secrets.*`, `*.key`
- Environment-specific configurations (PROD_KEY, SECRET, etc.)

**For environment variables, show:**
- Variable name only (e.g., `DATABASE_URL` → `"***REDACTED***"`)
- Type/format (e.g., "string", "URL", "port number")
- Whether it's required/optional
- Do NOT show actual values

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
├── resources.md                 # External resources, configs, env vars (redacted)
├── workflows.md                 # Build, test, deploy, CI/CD workflows
└── figures/
    └── [diagram-name].md       # Architecture diagrams (SVG reference)
```

### HTML Manual Output (`{project-root}/.claude/wiki/html/`)

```
.claude/wiki/html/
├── index.html                   # THE HOLY GRAIL — dark-themed manual with all SVGs embedded
├── styles.css                   # Dark theme styling
├── mindmap.svg                  # Interactive architecture mindmap (inline in index.html)
├── architecture.svg             # System architecture diagram (inline in index.html)
├── workflows.svg                # CI/CD workflow diagram (inline in index.html)
└── assets/
    └── (any supplementary assets)
```

## Generation Process

### Phase 1: Comprehensive Codebase Analysis

**Use Bash `find`/`ls` and Read tool to explore:**

1. **Project Structure**
   - Root directory layout
   - Source directories (`src/`, `lib/`, `app/`, etc.)
   - Configuration directories
   - Test directories
   - Documentation locations

2. **Source Files — Document EVERYTHING:**
   - All source files (`.ts`, `.js`, `.py`, `.go`, `.rs`, `.java`, `.cpp`, `.c`, etc.)
   - Internal utilities and helpers
   - Private functions and methods
   - Class implementations
   - Function signatures with parameters and return types
   - Type definitions and interfaces
   - Enums and constants

3. **Configuration Files:**
   - `package.json`, `pyproject.toml`, `Cargo.toml`, `go.mod`, etc.
   - Build configurations
   - Linting/formatting configs (ESLint, Prettier, etc.)
   - TypeScript config (`tsconfig.json`)
   - Environment config (NEVER show values from `.env`)
   - Docker configurations
   - CI/CD configurations

4. **API Endpoints — Complete Documentation:**
   For each endpoint, document:
   - **Route/Path** — Full path including parameters
   - **HTTP Method** — GET, POST, PUT, PATCH, DELETE, etc.
   - **Description** — What it does
   - **Authentication** — Required auth type (Bearer, API Key, OAuth, etc.)
   - **Request Headers** — Content-Type, Authorization, custom headers
   - **Request Body** — Schema, required fields, optional fields
   - **Request Parameters** — Path params, query params, headers
   - **Response Body** — Success response schema
   - **Response Codes** — 200, 201, 400, 401, 403, 404, 500, etc.
   - **Error Responses** — Each error code with message and solution
   - **Example Request** — curl command with sample data
   - **Example Response** — JSON response example

5. **Data Models:**
   - Database schemas
   - Entity relationships
   - Data structures
   - TypeScript interfaces/Java classes
   - Serialization formats

6. **Workflows:**
   - Build process and scripts
   - Test execution (unit, integration, e2e)
   - Deployment pipelines
   - CI/CD configuration
   - Development workflows

7. **Dependencies:**
   - External packages/libraries
   - Internal modules
   - Version constraints
   - Peer dependencies

### Phase 2: Create Directory Structure

```bash
mkdir -p .claude/wiki/modules
mkdir -p .claude/wiki/api
mkdir -p .claude/wiki/workflows
mkdir -p .claude/wiki/figures
mkdir -p .claude/wiki/html/assets
```

### Phase 3: Generate and Write ALL Files

#### SVG Diagrams to Generate

1. **`mindmap.svg`** — Architecture mindmap (interactive tree layout)
2. **`architecture.svg`** — System component diagram
3. **`workflows.svg`** — CI/CD build/deploy pipeline

#### Required Markdown Files:

1. **`.claude/wiki/README.md`** — Entry point
2. **`.claude/wiki/architecture.md`** — System design
3. **`.claude/wiki/modules/index.md`** — Module overview
4. **`.claude/wiki/modules/[module-name].md`** — Per module (EVERY module)
5. **`.claude/wiki/api/index.md`** — API overview
6. **`.claude/wiki/api/[endpoint-name].md`** — Per endpoint (EVERY endpoint)
7. **`.claude/wiki/patterns.md`** — Design patterns
8. **`.claude/wiki/resources.md`** — Configs (REDACTED)
9. **`.claude/wiki/workflows.md`** — CI/CD, builds, deployments

#### Required HTML Manual Files:

1. **`.claude/wiki/html/index.html`** — THE HOLY GRAIL dark-themed manual
2. **`.claude/wiki/html/styles.css`** — Dark theme styling

### Detailed File Specifications

#### SVG Diagram Generation

All SVGs must be hand-crafted SVG with:
- Dark theme colors (dark background, light text, accent colors)
- Clean node-based layouts
- Connecting lines/arrows between nodes
- Legend/color key where appropriate
- Viewbox for scalability

##### mindmap.svg Structure

```svg
<svg viewBox="0 0 1200 800" xmlns="http://www.w3.org/2000/svg">
  <!-- Dark background -->
  <rect width="100%" height="100%" fill="#0d1117"/>

  <!-- Central root node -->
  <g class="root">
    <rect x="500" y="20" width="200" height="50" rx="8" fill="#238636"/>
    <text x="600" y="52" text-anchor="middle" fill="#fff" font-family="system-ui">Project Name</text>
  </g>

  <!-- Main branches -->
  <g class="branch" data-label="Architecture">
    <!-- Branch node -->
    <rect x="50" y="100" width="150" height="40" rx="6" fill="#1f6feb"/>
    <text x="125" y="125" text-anchor="middle" fill="#fff">Architecture</text>
    <!-- Sub-branches -->
    <line x1="200" y1="120" x2="250" y2="180" stroke="#484f58" stroke-width="2"/>
    <rect x="250" y="160" width="120" height="35" rx="5" fill="#2d333b"/>
    <text x="310" y="183" text-anchor="middle" fill="#e6edf3">Core</text>
    <!-- etc -->
  </g>

  <!-- Connectors with curves -->
  <path d="M600,70 Q600,100 550,120" stroke="#484f58" fill="none" stroke-width="2"/>
</svg>
```

##### architecture.svg Structure

```svg
<svg viewBox="0 0 1000 600" xmlns="http://www.w3.org/2000/svg">
  <rect width="100%" height="100%" fill="#0d1117"/>

  <!-- Component boxes -->
  <g class="component" data-component="frontend">
    <rect x="50" y="50" width="200" height="120" rx="8" fill="#21262d" stroke="#30363d"/>
    <text x="150" y="80" text-anchor="middle" fill="#e6edf3" font-weight="bold">Frontend</text>
    <text x="150" y="105" text-anchor="middle" fill="#8b949e" font-size="12">React / Next.js</text>
    <rect x="70" y="120" width="160" height="30" rx="4" fill="#1f6feb" opacity="0.2"/>
    <text x="150" y="140" text-anchor="middle" fill="#58a6ff" font-size="11">Components</text>
  </g>

  <!-- Arrows between components -->
  <defs>
    <marker id="arrowhead" markerWidth="10" markerHeight="7" refX="9" refY="3.5" orient="auto">
      <polygon points="0 0, 10 3.5, 0 7" fill="#484f58"/>
    </marker>
  </defs>
  <line x1="250" y1="110" x2="350" y2="110" stroke="#484f58" stroke-width="2" marker-end="url(#arrowhead)"/>

  <!-- API Gateway -->
  <g class="component" data-component="api-gateway">
    <rect x="350" y="50" width="200" height="120" rx="8" fill="#21262d" stroke="#30363d"/>
    <text x="450" y="80" text-anchor="middle" fill="#e6edf3" font-weight="bold">API Gateway</text>
    <text x="450" y="105" text-anchor="middle" fill="#8b949e" font-size="12">Express / FastAPI</text>
  </g>

  <!-- Database -->
  <g class="component" data-component="database">
    <rect x="350" y="250" width="200" height="100" rx="8" fill="#21262d" stroke="#30363d"/>
    <text x="450" y="285" text-anchor="middle" fill="#e6edf3" font-weight="bold">Database</text>
    <text x="450" y="310" text-anchor="middle" fill="#8b949e" font-size="12">PostgreSQL / MongoDB</text>
  </g>

  <!-- Connectors -->
  <line x1="450" y1="170" x2="450" y2="250" stroke="#484f58" stroke-width="2" marker-end="url(#arrowhead)"/>
</svg>
```

##### workflows.svg Structure

```svg
<svg viewBox="0 0 1000 500" xmlns="http://www.w3.org/2000/svg">
  <rect width="100%" height="100%" fill="#0d1117"/>

  <!-- Pipeline stages as columns -->
  <g class="stage" data-stage="build">
    <rect x="30" y="30" width="180" height="440" rx="8" fill="#161b22" stroke="#30363d"/>
    <text x="120" y="60" text-anchor="middle" fill="#e6edf3" font-weight="bold" font-size="14">BUILD</text>

    <!-- Step boxes -->
    <rect x="50" y="90" width="140" height="50" rx="6" fill="#21262d"/>
    <text x="120" y="120" text-anchor="middle" fill="#58a6ff">Checkout</text>

    <rect x="50" y="160" width="140" height="50" rx="6" fill="#21262d"/>
    <text x="120" y="190" text-anchor="middle" fill="#58a6ff">Install</text>

    <rect x="50" y="230" width="140" height="50" rx="6" fill="#21262d"/>
    <text x="120" y="260" text-anchor="middle" fill="#58a6ff">Lint</text>

    <!-- Connectors within stage -->
    <line x1="120" y1="140" x2="120" y2="160" stroke="#484f58" stroke-width="2"/>
    <line x1="120" y1="210" x2="120" y2="230" stroke="#484f58" stroke-width="2"/>
  </g>

  <!-- Stage connectors (between columns) -->
  <line x1="210" y1="115" x2="250" y2="115" stroke="#238636" stroke-width="3"/>
  <polygon points="250,115 245,110 245,120" fill="#238636"/>
</svg>
```

#### index.html — THE HOLY GRAIL MANUAL

A single-page dark-themed HTML manual that embeds all SVG diagrams inline and provides comprehensive navigation to all documentation.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{Project Name} — The Holy Grail</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header>
        <nav class="sidebar">
            <div class="logo">{Project Name}</div>
            <ul class="nav-links">
                <li><a href="#overview">Overview</a></li>
                <li><a href="#mindmap">Mind Map</a></li>
                <li><a href="#architecture">Architecture</a></li>
                <li><a href="#workflows">Workflows</a></li>
                <li><a href="#modules">Modules</a></li>
                <li><a href="#api">API</a></li>
                <li><a href="#patterns">Patterns</a></li>
                <li><a href="#resources">Resources</a></li>
            </ul>
        </nav>
    </header>

    <main>
        <section id="overview" class="hero">
            <h1>{Project Name}</h1>
            <p class="tagline">The Holy Grail of Documentation</p>
            <div class="stats">
                <span>{N} Modules</span>
                <span>{N} API Endpoints</span>
                <span>{N} Files</span>
            </div>
        </section>

        <section id="mindmap">
            <h2>Architecture Mind Map</h2>
            <div class="diagram-container">
                <!-- Inline SVG mindmap -->
                <svg viewBox="0 0 1400 900" xmlns="http://www.w3.org/2000/svg">
                    <!-- Full dark theme mindmap SVG embedded inline -->
                </svg>
            </div>
        </section>

        <section id="architecture">
            <h2>System Architecture</h2>
            <div class="diagram-container">
                <!-- Inline SVG architecture diagram -->
                <svg viewBox="0 0 1200 700" xmlns="http://www.w3.org/2000/svg">
                    <!-- Full dark theme architecture SVG embedded inline -->
                </svg>
            </div>
        </section>

        <section id="workflows">
            <h2>CI/CD Workflows</h2>
            <div class="diagram-container">
                <!-- Inline SVG workflows diagram -->
                <svg viewBox="0 0 1200 600" xmlns="http://www.w3.org/2000/svg">
                    <!-- Full dark theme workflows SVG embedded inline -->
                </svg>
            </div>
        </section>

        <section id="modules">
            <h2>Modules</h2>
            <div class="grid">
                <!-- Module cards -->
            </div>
        </section>

        <section id="api">
            <h2>API Endpoints</h2>
            <div class="endpoints">
                <!-- Endpoint listings -->
            </div>
        </section>

        <section id="patterns">
            <h2>Patterns & Conventions</h2>
            <!-- Pattern documentation -->
        </section>

        <section id="resources">
            <h2>Resources & Configuration</h2>
            <!-- Redacted configuration -->
        </section>
    </main>

    <footer>
        <p>Generated on {date} · <a href="../README.md">View Markdown Version</a></p>
    </footer>
</body>
</html>
```

#### styles.css — Dark Theme

```css
:root {
    --bg-primary: #0d1117;
    --bg-secondary: #161b22;
    --bg-tertiary: #21262d;
    --border: #30363d;
    --text-primary: #e6edf3;
    --text-secondary: #8b949e;
    --accent-blue: #58a6ff;
    --accent-green: #238636;
    --accent-purple: #a371f7;
    --accent-orange: #d29922;
    --accent-red: #f85149;
}

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', system-ui, sans-serif;
    background-color: var(--bg-primary);
    color: var(--text-primary);
    line-height: 1.6;
}

.sidebar {
    position: fixed;
    left: 0;
    top: 0;
    width: 260px;
    height: 100vh;
    background: var(--bg-secondary);
    border-right: 1px solid var(--border);
    padding: 24px;
    overflow-y: auto;
}

.logo {
    font-size: 20px;
    font-weight: 700;
    color: var(--accent-green);
    margin-bottom: 32px;
}

.nav-links {
    list-style: none;
}

.nav-links li {
    margin-bottom: 8px;
}

.nav-links a {
    color: var(--text-secondary);
    text-decoration: none;
    padding: 8px 12px;
    border-radius: 6px;
    display: block;
    transition: all 0.2s;
}

.nav-links a:hover {
    background: var(--bg-tertiary);
    color: var(--text-primary);
}

main {
    margin-left: 260px;
    padding: 48px;
    max-width: 1200px;
}

section {
    margin-bottom: 80px;
}

.hero {
    text-align: center;
    padding: 80px 0;
}

.hero h1 {
    font-size: 56px;
    font-weight: 800;
    background: linear-gradient(135deg, var(--accent-blue), var(--accent-purple));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    margin-bottom: 16px;
}

.tagline {
    font-size: 24px;
    color: var(--text-secondary);
    margin-bottom: 32px;
}

.stats {
    display: flex;
    gap: 32px;
    justify-content: center;
}

.stats span {
    background: var(--bg-tertiary);
    padding: 12px 24px;
    border-radius: 8px;
    border: 1px solid var(--border);
}

h2 {
    font-size: 32px;
    font-weight: 700;
    margin-bottom: 24px;
    padding-bottom: 16px;
    border-bottom: 1px solid var(--border);
}

.diagram-container {
    background: var(--bg-secondary);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 24px;
    overflow-x: auto;
}

.diagram-container svg {
    width: 100%;
    height: auto;
    max-width: none;
}

.grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 20px;
}

.card {
    background: var(--bg-secondary);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 20px;
}

footer {
    text-align: center;
    padding: 48px;
    color: var(--text-secondary);
    border-top: 1px solid var(--border);
}
```

## Configuration Options

### Output Location
- Markdown: `{project-root}/.claude/wiki/`
- HTML Manual: `{project-root}/.claude/wiki/html/`

### Options
- `--force` — overwrite existing wiki
- `--modules-only` — only generate module docs
- `--api-only` — only generate API docs
- `--html-only` — skip markdown, only generate HTML
- `--mindmap-only` — only generate mindmap

## Quality Standards

1. **Completeness:**
   - Every module must have a page
   - Every function must be documented
   - Every API endpoint must have full documentation

2. **Accuracy:**
   - Code examples must be correct
   - Type signatures must match actual code
   - Cross-references must be valid

3. **Security:**
   - NEVER expose .env or secrets
   - Redact all sensitive values
   - Show only variable names and types

4. **Clarity:**
   - Use consistent formatting
   - Include code examples
   - Add cross-references between related items

5. **SVG Diagrams:**
   - All SVGs must use dark theme colors
   - ViewBox for scalability
   - Semantic grouping with `g` elements
   - Descriptive class/data attributes
   - Clean connecting lines with arrow markers
   - Accessible with title/desc elements

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
- Any file matching `.env*`, `secrets.*`, `*.key`, `*.pem`
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
├── mindmap.svg                  # Architecture mindmap (inline in index.html)
├── architecture.svg             # System architecture diagram (inline in index.html)
├── workflows.svg                # CI/CD workflow diagram (inline in index.html)
└── assets/
    └── (any supplementary assets)
```

## Generation Process

### Phase 1: Comprehensive Codebase Analysis

**Use Bash `find`/`ls` and Read tool to explore:**

For large repositories (roughly 200+ source files), read entry points, configs and public interfaces in full, sample the rest, and state in `README.md` which parts were sampled. Do not let the analysis run out of context partway through.

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
   - Environment config: do NOT open `.env` files. Take variable names from `.env.example` or from code references, and never show values
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

> The SVG and HTML snippets below are templates. Replace every label with facts from the repo you analyzed. Labels such as Jest, Redis, Stripe, PostgreSQL and PagerDuty are placeholders: do not copy them into the output unless the repo uses them.

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

All SVGs must be hand-crafted SVG with careful attention to **readability and non-overlapping layout**.

**Layout Principles:**
- Use a **grid-based layout** with explicit x/y coordinates — no automatic positioning
- **Space nodes apart** — minimum 40px horizontal gap between sibling nodes, 60px vertical gap between levels
- **Never overlap nodes** — calculate bounding boxes and ensure no intersection
- **Wrap long text** inside nodes or limit node width to prevent text overflow
- **Use a generous viewBox** that fits the content with comfortable margins (at least 60px padding on all sides)
- **Group related elements** in `<g>` with clear IDs — never dump all elements at the root level
- **Order layers deliberately** — background → connectors → nodes → labels

**Font & Text Rules:**
- Minimum **12px font size** for any text; use **14px+** for node titles
- Use `dominant-baseline: middle` and `text-anchor: middle` for centered node labels
- Keep node labels **short (under 30 chars)** — break longer labels across multiple lines using `<tspan>` or multiple `<text>` elements
- Never let text touch node borders — minimum **12px padding** inside rects
- Use a **monospace or system-ui font stack** for consistency

**Sizing & Spacing:**
- Node rects: minimum **100px wide × 40px tall** for leaf nodes, larger for parent nodes
- Corner radius (`rx`): **6–8px** for a clean look, never fully squared
- Stroke width: **1.5–2px** for outlines, **2–3px** for connector lines
- Arrow markers: defined in `<defs>`, sized at **10×7** with proper refX/refY

**Connector Rules:**
- Draw connectors **from edge to edge** of nodes, not center to center
- Use **right-angle paths** (horizontal then vertical, or vice versa) instead of diagonal lines — much easier to trace
- Avoid **3-way or 4-way connector intersections** — reroute paths to avoid crossing
- Add **15px clearance** around any connector crossing another node
- Connector color: `#30363d` or `#484f58` (subtle), never bright colors

**Color Palette:**
- Background: `#0d1117`
- Node fills: `#161b22` (standard), `#21262d` (highlighted), `#1f6feb` (info), `#238636` (success/root)
- Node borders: `#30363d`
- Text: `#e6edf3` (primary), `#8b949e` (secondary)
- Connectors: `#30363d`
- Accent arrows: `#484f58`

**Accessibility:**
- Every `<svg>` must have `<title>` and `<desc>`
- Interactive elements should have `role` and `aria-label`
- High contrast ratio — never put light text on light background or vice versa

##### mindmap.svg Structure

```svg
<svg viewBox="0 0 1400 900" xmlns="http://www.w3.org/2000/svg" role="img">
  <title>Architecture Mind Map</title>
  <desc>Hierarchical tree showing project architecture from root to leaf modules</desc>

  <!-- Arrow marker definition -->
  <defs>
    <marker id="arrow" markerWidth="10" markerHeight="7" refX="9" refY="3.5" orient="auto">
      <polygon points="0 0, 10 3.5, 0 7" fill="#30363d"/>
    </marker>
  </defs>

  <!-- Background -->
  <rect width="100%" height="100%" fill="#0d1117"/>

  <!-- LAYER 1: Root node (centered top) -->
  <g id="root">
    <rect x="600" y="30" width="200" height="55" rx="8" fill="#238636" stroke="#2ea043" stroke-width="1.5"/>
    <text x="700" y="63" text-anchor="middle" fill="#ffffff" font-size="16" font-weight="700">Project Name</text>
  </g>

  <!-- LAYER 2: Top-level branches (4 columns, well-spaced) -->
  <!-- Each branch is 300px wide with 40px gap from neighbors -->
  <!-- Branch: Architecture (x: 40–340) -->
  <g id="branch-architecture">
    <!-- Connector: root bottom (700,85) → branch top (190,160) -->
    <path d="M700,85 L700,120 L190,120 L190,145" stroke="#30363d" stroke-width="2" fill="none" marker-end="url(#arrow)"/>

    <rect x="90" y="145" width="200" height="45" rx="6" fill="#1f6feb" stroke="#388bfd" stroke-width="1.5"/>
    <text x="190" y="173" text-anchor="middle" fill="#ffffff" font-size="14" font-weight="600">Architecture</text>

    <!-- Sub-nodes (vertically stacked, 70px apart) -->
    <!-- Sub: Core (x: 40–340, y: 215) -->
    <rect x="40" y="215" width="130" height="40" rx="5" fill="#21262d" stroke="#30363d"/>
    <text x="105" y="242" text-anchor="middle" fill="#e6edf3" font-size="13">Core</text>

    <!-- Sub: Data Layer -->
    <rect x="190" y="215" width="130" height="40" rx="5" fill="#21262d" stroke="#30363d"/>
    <text x="255" y="242" text-anchor="middle" fill="#e6edf3" font-size="13">Data Layer</text>

    <!-- Sub-sub nodes (beneath Core, y: 280) -->
    <path d="M105,255 L105,275" stroke="#30363d" stroke-width="1.5" fill="none" marker-end="url(#arrow)"/>
    <rect x="40" y="280" width="130" height="35" rx="4" fill="#161b22" stroke="#30363d"/>
    <text x="105" y="304" text-anchor="middle" fill="#8b949e" font-size="12">Database</text>

    <!-- Sub-sub nodes (beneath Data Layer, y: 280) -->
    <path d="M255,255 L255,275" stroke="#30363d" stroke-width="1.5" fill="none" marker-end="url(#arrow)"/>
    <rect x="190" y="280" width="130" height="35" rx="4" fill="#161b22" stroke="#30363d"/>
    <text x="255" y="304" text-anchor="middle" fill="#8b949e" font-size="12">Models</text>
  </g>

  <!-- Branch: API (x: 380–680) -->
  <g id="branch-api">
    <path d="M700,85 L700,120 L530,120 L530,145" stroke="#30363d" stroke-width="2" fill="none" marker-end="url(#arrow)"/>

    <rect x="430" y="145" width="200" height="45" rx="6" fill="#a371f7" stroke="#8b5cf6" stroke-width="1.5"/>
    <text x="530" y="173" text-anchor="middle" fill="#ffffff" font-size="14" font-weight="600">API Endpoints</text>

    <!-- API sub-nodes (vertically stacked) -->
    <rect x="430" y="215" width="90" height="40" rx="5" fill="#21262d" stroke="#30363d"/>
    <text x="475" y="242" text-anchor="middle" fill="#e6edf3" font-size="12">/users</text>

    <rect x="540" y="215" width="90" height="40" rx="5" fill="#21262d" stroke="#30363d"/>
    <text x="585" y="242" text-anchor="middle" fill="#e6edf3" font-size="12">/orders</text>
  </g>

  <!-- Branch: Workflows (x: 720–1020) -->
  <g id="branch-workflows">
    <path d="M700,85 L700,120 L870,120 L870,145" stroke="#30363d" stroke-width="2" fill="none" marker-end="url(#arrow)"/>

    <rect x="770" y="145" width="200" height="45" rx="6" fill="#d29922" stroke="#e3b341" stroke-width="1.5"/>
    <text x="870" y="173" text-anchor="middle" fill="#ffffff" font-size="14" font-weight="600">Workflows</text>

    <rect x="770" y="215" width="90" height="40" rx="5" fill="#21262d" stroke="#30363d"/>
    <text x="815" y="242" text-anchor="middle" fill="#e6edf3" font-size="12">Build</text>

    <rect x="880" y="215" width="90" height="40" rx="5" fill="#21262d" stroke="#30363d"/>
    <text x="925" y="242" text-anchor="middle" fill="#e6edf3" font-size="12">Deploy</text>
  </g>

  <!-- Branch: Patterns (x: 1060–1260) -->
  <g id="branch-patterns">
    <path d="M700,85 L700,120 L1130,120 L1130,145" stroke="#30363d" stroke-width="2" fill="none" marker-end="url(#arrow)"/>

    <rect x="1030" y="145" width="200" height="45" rx="6" fill="#f85149" stroke="#ff7b72" stroke-width="1.5"/>
    <text x="1130" y="173" text-anchor="middle" fill="#ffffff" font-size="14" font-weight="600">Patterns</text>

    <rect x="1030" y="215" width="200" height="40" rx="5" fill="#21262d" stroke="#30363d"/>
    <text x="1130" y="242" text-anchor="middle" fill="#e6edf3" font-size="12">Design Patterns</text>
  </g>
</svg>
```

##### architecture.svg Structure

```svg
<svg viewBox="0 0 1200 700" xmlns="http://www.w3.org/2000/svg" role="img">
  <title>System Architecture</title>
  <desc>Component diagram showing system layers and data flow</desc>

  <defs>
    <marker id="arrowhead" markerWidth="10" markerHeight="7" refX="9" refY="3.5" orient="auto">
      <polygon points="0 0, 10 3.5, 0 7" fill="#484f58"/>
    </marker>
    <marker id="arrowhead-green" markerWidth="10" markerHeight="7" refX="9" refY="3.5" orient="auto">
      <polygon points="0 0, 10 3.5, 0 7" fill="#238636"/>
    </marker>
  </defs>

  <!-- Background -->
  <rect width="100%" height="100%" fill="#0d1117"/>

  <!-- LAYER: External (top row, y: 40) -->
  <g id="layer-external">
    <!-- Client -->
    <g id="client">
      <rect x="60" y="40" width="160" height="80" rx="8" fill="#21262d" stroke="#30363d" stroke-width="1.5"/>
      <text x="140" y="70" text-anchor="middle" fill="#e6edf3" font-size="14" font-weight="600">Client</text>
      <text x="140" y="90" text-anchor="middle" fill="#8b949e" font-size="12">Browser / Mobile</text>
    </g>

    <!-- Third-party Services -->
    <g id="external-services">
      <rect x="980" y="40" width="160" height="80" rx="8" fill="#21262d" stroke="#30363d" stroke-width="1.5"/>
      <text x="1060" y="70" text-anchor="middle" fill="#e6edf3" font-size="14" font-weight="600">External APIs</text>
      <text x="1060" y="90" text-anchor="middle" fill="#8b949e" font-size="12">Stripe, SendGrid</text>
    </g>
  </g>

  <!-- LAYER: Application (middle row, y: 180) -->
  <g id="layer-application">
    <!-- API Gateway -->
    <g id="api-gateway">
      <rect x="420" y="180" width="360" height="100" rx="8" fill="#21262d" stroke="#30363d" stroke-width="1.5"/>
      <text x="600" y="215" text-anchor="middle" fill="#e6edf3" font-size="15" font-weight="700">API Gateway</text>
      <text x="600" y="238" text-anchor="middle" fill="#8b949e" font-size="12">Express / FastAPI · Auth · Rate Limit</text>
    </g>

    <!-- Services (split into columns) -->
    <!-- Auth Service -->
    <g id="auth-service">
      <rect x="80" y="330" width="180" height="90" rx="8" fill="#21262d" stroke="#30363d" stroke-width="1.5"/>
      <text x="170" y="365" text-anchor="middle" fill="#e6edf3" font-size="14" font-weight="600">Auth Service</text>
      <text x="170" y="388" text-anchor="middle" fill="#8b949e" font-size="12">JWT · Sessions</text>
    </g>

    <!-- User Service -->
    <g id="user-service">
      <rect x="290" y="330" width="180" height="90" rx="8" fill="#21262d" stroke="#30363d" stroke-width="1.5"/>
      <text x="380" y="365" text-anchor="middle" fill="#e6edf3" font-size="14" font-weight="600">User Service</text>
      <text x="380" y="388" text-anchor="middle" fill="#8b949e" font-size="12">CRUD · Profiles</text>
    </g>

    <!-- Order Service -->
    <g id="order-service">
      <rect x="500" y="330" width="180" height="90" rx="8" fill="#21262d" stroke="#30363d" stroke-width="1.5"/>
      <text x="590" y="365" text-anchor="middle" fill="#e6edf3" font-size="14" font-weight="600">Order Service</text>
      <text x="590" y="388" text-anchor="middle" fill="#8b949e" font-size="12">Checkout · Cart</text>
    </g>

    <!-- Product Service -->
    <g id="product-service">
      <rect x="710" y="330" width="180" height="90" rx="8" fill="#21262d" stroke="#30363d" stroke-width="1.5"/>
      <text x="800" y="365" text-anchor="middle" fill="#e6edf3" font-size="14" font-weight="600">Product Service</text>
      <text x="800" y="388" text-anchor="middle" fill="#8b949e" font-size="12">Catalog · Search</text>
    </g>
  </g>

  <!-- LAYER: Data (bottom row, y: 480) -->
  <g id="layer-data">
    <!-- Primary DB -->
    <g id="primary-db">
      <rect x="290" y="480" width="200" height="80" rx="8" fill="#21262d" stroke="#238636" stroke-width="1.5"/>
      <text x="390" y="515" text-anchor="middle" fill="#e6edf3" font-size="14" font-weight="600">PostgreSQL</text>
      <text x="390" y="538" text-anchor="middle" fill="#8b949e" font-size="12">Primary Store</text>
    </g>

    <!-- Cache -->
    <g id="cache">
      <rect x="520" y="480" width="160" height="80" rx="8" fill="#21262d" stroke="#d29922" stroke-width="1.5"/>
      <text x="600" y="515" text-anchor="middle" fill="#e6edf3" font-size="14" font-weight="600">Redis</text>
      <text x="600" y="538" text-anchor="middle" fill="#8b949e" font-size="12">Cache · Queue</text>
    </g>

    <!-- Object Storage -->
    <g id="storage">
      <rect x="710" y="480" width="180" height="80" rx="8" fill="#21262d" stroke="#30363d" stroke-width="1.5"/>
      <text x="800" y="515" text-anchor="middle" fill="#e6edf3" font-size="14" font-weight="600">S3 / R2</text>
      <text x="800" y="538" text-anchor="middle" fill="#8b949e" font-size="12">Files · Media</text>
    </g>
  </g>

  <!-- CONNECTORS (drawn after all nodes so they appear beneath) -->
  <g id="connectors">
    <!-- Client → API Gateway -->
    <path d="M220,80 L420,80" stroke="#484f58" stroke-width="2" fill="none" marker-end="url(#arrowhead)"/>

    <!-- API Gateway → Services -->
    <path d="M420,250 L380,250 L380,330" stroke="#484f58" stroke-width="1.5" fill="none" marker-end="url(#arrowhead)"/>
    <path d="M600,280 L600,330" stroke="#484f58" stroke-width="1.5" fill="none" marker-end="url(#arrowhead)"/>
    <path d="M780,250 L800,250 L800,330" stroke="#484f58" stroke-width="1.5" fill="none" marker-end="url(#arrowhead)"/>

    <!-- Services → Data Layer (right-angle paths) -->
    <path d="M380,420 L380,480" stroke="#484f58" stroke-width="1.5" fill="none" marker-end="url(#arrowhead-green)"/>
    <path d="M590,420 L590,480" stroke="#484f58" stroke-width="1.5" fill="none" marker-end="url(#arrowhead)"/>
    <path d="M800,420 L800,480" stroke="#484f58" stroke-width="1.5" fill="none" marker-end="url(#arrowhead)"/>

    <!-- External → Services (right-angle) -->
    <path d="M980,80 L980,200 L890,200 L890,330" stroke="#484f58" stroke-width="1.5" fill="none" marker-end="url(#arrowhead)"/>
  </g>

  <!-- LEGEND -->
  <g id="legend" transform="translate(60, 600)">
    <text x="0" y="0" fill="#8b949e" font-size="12" font-weight="600">LEGEND</text>
    <rect x="0" y="10" width="16" height="16" rx="3" fill="#21262d" stroke="#238636"/>
    <text x="24" y="23" fill="#8b949e" font-size="12">Primary Data</text>
    <rect x="110" y="10" width="16" height="16" rx="3" fill="#21262d" stroke="#d29922"/>
    <text x="134" y="23" fill="#8b949e" font-size="12">Cache / Queue</text>
    <rect x="220" y="10" width="16" height="16" rx="3" fill="#21262d" stroke="#30363d"/>
    <text x="244" y="23" fill="#8b949e" font-size="12">Standard</text>
  </g>
</svg>
```

##### workflows.svg Structure

```svg
<svg viewBox="0 0 1200 600" xmlns="http://www.w3.org/2000/svg" role="img">
  <title>CI/CD Workflows</title>
  <desc>Pipeline diagram showing build, test, and deploy stages</desc>

  <defs>
    <marker id="flow-arrow" markerWidth="10" markerHeight="7" refX="9" refY="3.5" orient="auto">
      <polygon points="0 0, 10 3.5, 0 7" fill="#30363d"/>
    </marker>
    <marker id="flow-arrow-green" markerWidth="10" markerHeight="7" refX="9" refY="3.5" orient="auto">
      <polygon points="0 0, 10 3.5, 0 7" fill="#238636"/>
    </marker>
    <marker id="flow-arrow-red" markerWidth="10" markerHeight="7" refX="9" refY="3.5" orient="auto">
      <polygon points="0 0, 10 3.5, 0 7" fill="#f85149"/>
    </marker>
  </defs>

  <!-- Background -->
  <rect width="100%" height="100%" fill="#0d1117"/>

  <!-- STAGE COLUMNS: 4 stages, each 240px wide with 40px gaps -->
  <!-- Column widths: 60px padding + step width + 60px margin -->

  <!-- STAGE 1: Build (x: 40–280) -->
  <g id="stage-build">
    <rect x="40" y="40" width="240" height="520" rx="10" fill="#161b22" stroke="#30363d" stroke-width="1.5"/>
    <text x="160" y="70" text-anchor="middle" fill="#58a6ff" font-size="14" font-weight="700" letter-spacing="1">BUILD</text>

    <!-- Step: Checkout -->
    <g id="step-checkout">
      <rect x="70" y="100" width="180" height="60" rx="6" fill="#21262d" stroke="#30363d" stroke-width="1.5"/>
      <text x="160" y="130" text-anchor="middle" fill="#e6edf3" font-size="13" font-weight="500">Checkout</text>
      <text x="160" y="148" text-anchor="middle" fill="#8b949e" font-size="12">git clone</text>
    </g>

    <!-- Connector -->
    <line x1="160" y1="160" x2="160" y2="185" stroke="#30363d" stroke-width="2" marker-end="url(#flow-arrow)"/>

    <!-- Step: Install -->
    <g id="step-install">
      <rect x="70" y="185" width="180" height="60" rx="6" fill="#21262d" stroke="#30363d" stroke-width="1.5"/>
      <text x="160" y="215" text-anchor="middle" fill="#e6edf3" font-size="13" font-weight="500">Install</text>
      <text x="160" y="233" text-anchor="middle" fill="#8b949e" font-size="12">npm ci</text>
    </g>

    <!-- Connector -->
    <line x1="160" y1="245" x2="160" y2="270" stroke="#30363d" stroke-width="2" marker-end="url(#flow-arrow)"/>

    <!-- Step: Lint -->
    <g id="step-lint">
      <rect x="70" y="270" width="180" height="60" rx="6" fill="#21262d" stroke="#30363d" stroke-width="1.5"/>
      <text x="160" y="300" text-anchor="middle" fill="#e6edf3" font-size="13" font-weight="500">Lint</text>
      <text x="160" y="318" text-anchor="middle" fill="#8b949e" font-size="12">ESLint · Prettier</text>
    </g>

    <!-- Connector -->
    <line x1="160" y1="330" x2="160" y2="355" stroke="#30363d" stroke-width="2" marker-end="url(#flow-arrow)"/>

    <!-- Step: Compile -->
    <g id="step-compile">
      <rect x="70" y="355" width="180" height="60" rx="6" fill="#21262d" stroke="#30363d" stroke-width="1.5"/>
      <text x="160" y="385" text-anchor="middle" fill="#e6edf3" font-size="13" font-weight="500">Compile</text>
      <text x="160" y="403" text-anchor="middle" fill="#8b949e" font-size="12">tsc / webpack</text>
    </g>

    <!-- Connector -->
    <line x1="160" y1="415" x2="160" y2="440" stroke="#30363d" stroke-width="2" marker-end="url(#flow-arrow)"/>

    <!-- Step: Bundle -->
    <g id="step-bundle">
      <rect x="70" y="440" width="180" height="60" rx="6" fill="#21262d" stroke="#30363d" stroke-width="1.5"/>
      <text x="160" y="470" text-anchor="middle" fill="#e6edf3" font-size="13" font-weight="500">Bundle</text>
      <text x="160" y="488" text-anchor="middle" fill="#8b949e" font-size="12">minify · assets</text>
    </g>
  </g>

  <!-- STAGE 2: Test (x: 320–560) -->
  <g id="stage-test">
    <rect x="320" y="40" width="240" height="520" rx="10" fill="#161b22" stroke="#30363d" stroke-width="1.5"/>
    <text x="440" y="70" text-anchor="middle" fill="#a371f7" font-size="14" font-weight="700" letter-spacing="1">TEST</text>

    <g id="step-unit">
      <rect x="350" y="100" width="180" height="60" rx="6" fill="#21262d" stroke="#30363d" stroke-width="1.5"/>
      <text x="440" y="130" text-anchor="middle" fill="#e6edf3" font-size="13" font-weight="500">Unit Tests</text>
      <text x="440" y="148" text-anchor="middle" fill="#8b949e" font-size="12">Jest · 450+ tests</text>
    </g>

    <line x1="440" y1="160" x2="440" y2="185" stroke="#30363d" stroke-width="2" marker-end="url(#flow-arrow)"/>

    <g id="step-integration">
      <rect x="350" y="185" width="180" height="60" rx="6" fill="#21262d" stroke="#30363d" stroke-width="1.5"/>
      <text x="440" y="215" text-anchor="middle" fill="#e6edf3" font-size="13" font-weight="500">Integration</text>
      <text x="440" y="233" text-anchor="middle" fill="#8b949e" font-size="12">API tests</text>
    </g>

    <line x1="440" y1="245" x2="440" y2="270" stroke="#30363d" stroke-width="2" marker-end="url(#flow-arrow)"/>

    <g id="step-e2e">
      <rect x="350" y="270" width="180" height="60" rx="6" fill="#21262d" stroke="#30363d" stroke-width="1.5"/>
      <text x="440" y="300" text-anchor="middle" fill="#e6edf3" font-size="13" font-weight="500">E2E Tests</text>
      <text x="440" y="318" text-anchor="middle" fill="#8b949e" font-size="12">Playwright</text>
    </g>

    <line x1="440" y1="330" x2="440" y2="355" stroke="#30363d" stroke-width="2" marker-end="url(#flow-arrow)"/>

    <g id="step-security">
      <rect x="350" y="355" width="180" height="60" rx="6" fill="#21262d" stroke="#30363d" stroke-width="1.5"/>
      <text x="440" y="385" text-anchor="middle" fill="#e6edf3" font-size="13" font-weight="500">Security Scan</text>
      <text x="440" y="403" text-anchor="middle" fill="#8b949e" font-size="12">Snyk · Semgrep</text>
    </g>
  </g>

  <!-- INTER-STAGE CONNECTORS -->
  <!-- Build → Test -->
  <path d="M280,60 L320,60" stroke="#238636" stroke-width="3" fill="none" marker-end="url(#flow-arrow-green)"/>

  <!-- STAGE 3: Deploy (x: 600–840) -->
  <g id="stage-deploy">
    <rect x="600" y="40" width="240" height="520" rx="10" fill="#161b22" stroke="#30363d" stroke-width="1.5"/>
    <text x="720" y="70" text-anchor="middle" fill="#238636" font-size="14" font-weight="700" letter-spacing="1">DEPLOY</text>

    <g id="step-build-image">
      <rect x="630" y="100" width="180" height="60" rx="6" fill="#21262d" stroke="#30363d" stroke-width="1.5"/>
      <text x="720" y="130" text-anchor="middle" fill="#e6edf3" font-size="13" font-weight="500">Build Image</text>
      <text x="720" y="148" text-anchor="middle" fill="#8b949e" font-size="12">Docker · BuildKit</text>
    </g>

    <line x1="720" y1="160" x2="720" y2="185" stroke="#30363d" stroke-width="2" marker-end="url(#flow-arrow)"/>

    <g id="step-staging">
      <rect x="630" y="185" width="180" height="60" rx="6" fill="#21262d" stroke="#d29922" stroke-width="1.5"/>
      <text x="720" y="215" text-anchor="middle" fill="#e6edf3" font-size="13" font-weight="500">Deploy Staging</text>
      <text x="720" y="233" text-anchor="middle" fill="#8b949e" font-size="12">Auto deploy</text>
    </g>

    <line x1="720" y1="245" x2="720" y2="270" stroke="#30363d" stroke-width="2" marker-end="url(#flow-arrow)"/>

    <g id="step-smoke">
      <rect x="630" y="270" width="180" height="60" rx="6" fill="#21262d" stroke="#30363d" stroke-width="1.5"/>
      <text x="720" y="300" text-anchor="middle" fill="#e6edf3" font-size="13" font-weight="500">Smoke Tests</text>
      <text x="720" y="318" text-anchor="middle" fill="#8b949e" font-size="12">Health checks</text>
    </g>

    <line x1="720" y1="330" x2="720" y2="355" stroke="#30363d" stroke-width="2" marker-end="url(#flow-arrow)"/>

    <g id="step-production">
      <rect x="630" y="355" width="180" height="60" rx="6" fill="#21262d" stroke="#238636" stroke-width="1.5"/>
      <text x="720" y="385" text-anchor="middle" fill="#e6edf3" font-size="13" font-weight="500">Deploy Production</text>
      <text x="720" y="403" text-anchor="middle" fill="#8b949e" font-size="12">Blue-green</text>
    </g>
  </g>

  <!-- INTER-STAGE CONNECTOR: Test → Deploy -->
  <path d="M560,60 L600,60" stroke="#238636" stroke-width="3" fill="none" marker-end="url(#flow-arrow-green)"/>

  <!-- STAGE 4: Monitor (x: 880–1120) -->
  <g id="stage-monitor">
    <rect x="880" y="40" width="240" height="520" rx="10" fill="#161b22" stroke="#30363d" stroke-width="1.5"/>
    <text x="1000" y="70" text-anchor="middle" fill="#8b949e" font-size="14" font-weight="700" letter-spacing="1">MONITOR</text>

    <g id="step-metrics">
      <rect x="910" y="100" width="180" height="60" rx="6" fill="#21262d" stroke="#30363d" stroke-width="1.5"/>
      <text x="1000" y="130" text-anchor="middle" fill="#e6edf3" font-size="13" font-weight="500">Metrics</text>
      <text x="1000" y="148" text-anchor="middle" fill="#8b949e" font-size="12">Prometheus</text>
    </g>

    <line x1="1000" y1="160" x2="1000" y2="185" stroke="#30363d" stroke-width="2" marker-end="url(#flow-arrow)"/>

    <g id="step-logs">
      <rect x="910" y="185" width="180" height="60" rx="6" fill="#21262d" stroke="#30363d" stroke-width="1.5"/>
      <text x="1000" y="215" text-anchor="middle" fill="#e6edf3" font-size="13" font-weight="500">Logs</text>
      <text x="1000" y="233" text-anchor="middle" fill="#8b949e" font-size="12">Loki · Grafana</text>
    </g>

    <line x1="1000" y1="245" x2="1000" y2="270" stroke="#30363d" stroke-width="2" marker-end="url(#flow-arrow)"/>

    <g id="step-alerts">
      <rect x="910" y="270" width="180" height="60" rx="6" fill="#21262d" stroke="#f85149" stroke-width="1.5"/>
      <text x="1000" y="300" text-anchor="middle" fill="#e6edf3" font-size="13" font-weight="500">Alerts</text>
      <text x="1000" y="318" text-anchor="middle" fill="#8b949e" font-size="12">PagerDuty</text>
    </g>
  </g>

  <!-- INTER-STAGE CONNECTOR: Deploy → Monitor -->
  <path d="M840,60 L880,60" stroke="#30363d" stroke-width="2" fill="none" marker-end="url(#flow-arrow)"/>
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
- `--force` — overwrite an existing `.claude/wiki/`. Without it, if the folder already exists, stop and ask before writing anything
- `--modules-only` — write `modules/` pages and `README.md` only
- `--api-only` — write `api/` pages and `README.md` only
- `--html-only` — skip the markdown pages and generate `html/` only
- `--svg-only` — regenerate only `html/mindmap.svg`, `html/architecture.svg` and `html/workflows.svg`

## Quality Standards

1. **Completeness:**
   - Every module must have a page
   - Every public module, class, function and API endpoint is documented. Private helpers are grouped under their module page
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

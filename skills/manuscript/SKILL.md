---
name: manuscript
description: Conduct deep codebase analysis, cross-reference with existing wiki documentation, and produce a detailed research manuscript with LaTeX equations, citations, and academic formatting. Trigger on /manuscript or when user asks to create a research paper, technical report, or academic manuscript about the codebase.
---

# Manuscript — Research Documentation Generator

Produces a comprehensive, academically-styled research manuscript about the codebase, integrating deep code analysis with LaTeX-formatted equations, formal citations, and publication-ready structure.

**IMPORTANT:** When this skill is invoked, you MUST:
1. Conduct deep codebase exploration — EVERYTHING including internal details
2. Cross-reference with existing wiki at `.claude/wiki/` if available
3. Create ACTUAL files using Write tool — do not just describe what to generate
4. Include BOTH real academic citations AND placeholder citations for user to fill in
5. NEVER expose `.env` files, secrets, API keys, or sensitive configuration values

## Trigger Conditions

- User invokes `/manuscript`
- User asks to "create a research paper", "write a technical report", "generate a manuscript"
- User requests an "academic analysis", "formal documentation", or "detailed study" of the codebase
- User wants to "document with equations", "add citations", or "produce a paper"

## SECURITY — Never Expose These

**ALWAYS REDACT IN MANUSCRIPT:**
- `.env` files and environment variables
- API keys, tokens, secrets
- Passwords and credentials
- Database connection strings
- Private keys and certificates
- Any sensitive configuration

## Output Structure

### Files to Create (`{project-root}/.claude/manuscript/`)

```
.claude/manuscript/
├── manuscript.tex              # Main LaTeX document
├── references.bib              # Bibliography (BibTeX — real citations)
├── references-placeholder.bib  # Placeholder citations for user
├── Makefile                    # Compilation helper
├── abstract.tex                # Separate abstract file
├── figures/
│   ├── architecture.tex        # Architecture diagram (TikZ/Mermaid)
│   ├── dataflow.tex            # Data flow diagram
│   ├── statemachine.tex        # State machine diagram
│   ├── classdiagram.tex        # Class hierarchy diagram
│   └── network.tex             # Network/system diagram
└── tables/
    ├── api-endpoints.tex       # API endpoints table
    └── module-deps.tex         # Module dependencies table
```

## Generation Process

### Phase 1: Deep Codebase Exploration

**Use Bash `find`/`ls` and Read tool to thoroughly analyze:**

#### 1. Structural Analysis
- `ls` the project structure recursively
- Read ALL source files (`.ts`, `.js`, `.py`, `.go`, `.rs`, `.java`, `.cpp`, etc.)
- Map directory structure and module organization
- Identify entry points and main components
- Document EVERY function, class, interface, constant

#### 2. Semantic Analysis
- Understand core algorithms and data transformations
- Trace data flow through the system
- Identify state management patterns
- Map API contracts and interfaces
- Document complexity of key algorithms

#### 3. Pattern Recognition
- Design patterns in use (GoF, architectural patterns)
- Concurrency patterns (if applicable)
- Data persistence patterns
- Communication patterns (sync, async, event-driven)
- ML patterns (if applicable): model architecture, training loops, etc.

#### 4. Workflow Mapping
- Build processes
- Test execution flows
- Deployment pipelines
- CI/CD workflows

#### 5. ML-Specific Analysis (if project contains ML components)
For ML projects, document:
- **Model Architecture:**
  - Network topology (layers, connections)
  - Input/output shapes
  - Parameter counts
  - Pre-trained weights / fine-tuning approach
- **Loss Functions:**
  - Primary loss (CrossEntropy, MSE, etc.)
  - Auxiliary losses
  - Custom loss implementations
- **Optimizers:**
  - Optimizer type (Adam, SGD, etc.)
  - Learning rate schedule
  - Momentum, weight decay
  - Gradient clipping
- **Training Loop:**
  - Batch size, epochs
  - Data augmentation
  - Regularization (dropout, L2)
  - Early stopping criteria
- **Evaluation Metrics:**
  - Accuracy, precision, recall
  - Custom metrics
  - Benchmark datasets

### Phase 2: Wiki Cross-Reference

If `.claude/wiki/` exists:
1. Read existing documentation files
2. Cross-validate understanding
3. Use as foundation — expand abbreviated docs with deep analysis
4. Add mathematical formalization to described concepts

### Phase 3: Generate All Manuscript Files

#### 1. manuscript.tex — Complete LaTeX Document

```latex
\documentclass[10pt, conference]{IEEEtran}
%\documentclass[12pt, a4paper, oneside]{article}  % For ACM format

\usepackage[utf8]{inputenc}
\usepackage{amsmath, amssymb, graphicx, hyperref}
\usepackage{cite}
\usepackage[left=1in, right=1in, top=1in, bottom=1in]{geometry}
\usepackage{listings}
\usepackage{xcolor}

% Custom commands
\newcommand{\R}{\mathbb{R}}
\newcommand{\N}{\mathbb{N}}

\title{Systematic Analysis of {Project Name}: A Comprehensive Technical Survey}
\author{
    \IEEEauthorblockN{Generated by Claude Code}
    \IEEEauthorblockA{\textit{Technical Report}} \\
    \IEEEauthorblockA{\today}
}

\begin{document}

\maketitle

\input{abstract}

\section{Introduction}
\label{sec:introduction}
\input{introduction.tex}

\section{Background and Related Work}
\label{sec:background}
\input{background.tex}

\section{System Architecture}
\label{sec:architecture}
\input{architecture.tex}

\section{Implementation Details}
\label{sec:implementation}
\input{implementation.tex}

\section{Mathematical Foundations}
\label{sec:mathematics}
\input{mathematics.tex}

\section{Performance Analysis}
\label{sec:performance}
\input{performance.tex}

\section{Discussion}
\label{sec:discussion}
\input{discussion.tex}

\section{Conclusion and Future Work}
\label{sec:conclusion}
\input{conclusion.tex}

\bibliography{references}
\bibliographystyle{IEEEtran}  % For IEEE format
%\bibliographystyle{acm}       % For ACM format

\end{document}
```

#### 2. references.bib — Real Academic Citations

Include these real citations AND add placeholders:

```bibtex
% Design Patterns
@article{gamma1994design,
    author = {Gamma, Erich and Helm, Richard and Johnson, Ralph and Vlissides, John},
    title = {Design Patterns: Elements of Reusable Object-Oriented Software},
    journal = {Communications of the ACM},
    volume = {38},
    number = {10},
    pages = {30--35},
    year = {1994},
    doi = {10.1145/177669.177673}
}

% Software Architecture
@article{clements2001documenting,
    author = {Clements, Paul and Kazman, Rick and Klein, Mark},
    title = {Evaluating Software Architectures: Methods and Case Studies},
    journal = { Addison-Wesley Professional},
    year = {2001},
    publisher = {Addison-Wesley}
}

% API Design
@article{fielding2000architectural,
    author = {Fielding, Roy Thomas},
    title = {Architectural Styles and the Design of Network-based Software Architectures},
    journal = {University of California, Irvine},
    year = {2000},
    note = {Ph.D. dissertation}
}

% State Machines
@article{harel1987statecharts,
    author = {Harel, David},
    title = {Statecharts: A Visual Formalism for Complex Systems},
    journal = {Science of Computer Programming},
    volume = {8},
    number = {3},
    pages = {231--274},
    year = {1987},
    doi = {10.1016/0167-6423(87)90035-9}
}

% Complexity Analysis
@article{cormen2009introduction,
    author = {Cormen, Thomas H. and Leiserson, Charles E. and Rivest, Ronald L. and Stein, Clifford},
    title = {Introduction to Algorithms},
    journal = {MIT Press},
    edition = {Third},
    year = {2009}
}

% Machine Learning
@article{goodfellow2016deep,
    author = {Goodfellow, Ian and Bengio, Yoshua and Courville, Aaron},
    title = {Deep Learning},
    journal = {MIT Press},
    year = {2016},
    url = {https://www.deeplearningbook.org}
}

@article{lecun2015deep,
    author = {LeCun, Yann and Bengio, Yoshua and Hinton, Geoffrey},
    title = {Deep Learning},
    journal = {Nature},
    volume = {521},
    pages = {436--444},
    year = {2015},
    doi = {10.1038/nature14539}
}

% Optimization
@article{kingma2014adam,
    author = {Kingma, Diederik P. and Ba, Jimmy},
    title = {Adam: A Method for Stochastic Optimization},
    journal = {arXiv preprint arXiv:1412.6980},
    year = {2014}
}

% Data Flow
@article{abelson1996structure,
    author = {Abelson, Harold and Sussman, Gerald Jay and Sussman, Julie},
    title = {Structure and Interpretation of Computer Programs},
    journal = {MIT Press},
    year = {1996},
    edition = {Second}
}

% Network Architectures
@article{szegedy2015going,
    author = {Szegedy, Christian and Liu, Wei and Jia, Yangqing and others},
    title = {Going Deeper with Convolutions},
    journal = {Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition},
    pages = {1--9},
    year = {2015}
}

% Citation placeholder for user to fill
@article{CUSTOM-CITATION-1,
    author = {[AUTHOR NAME]},
    title = {[PAPER TITLE]},
    journal = {[JOURNAL/CONFERENCE]},
    year = {[YEAR]},
    note = {[OPTIONAL DOI OR URL]}
}
```

#### 3. references-placeholder.bib — For User to Fill

```bibtex
% Add your own citations here

@article{YOUR-CITATION-1,
    author = {First Author and Second Author},
    title = {Your Paper Title},
    journal = {Journal Name},
    volume = {1},
    number = {1},
    pages = {1--10},
    year = {2024},
    doi = {10.0000/example}
}

% Example for replacing with project-specific citations
@article{PROJECT-CITATION-1,
    author = {[Your Name]},
    title = {[Title of Related Paper]},
    journal = {[Conference/Journal Name]},
    year = {2024}
}
```

#### 4. mathematics.tex — All Equation Types

```latex
\section{Mathematical Foundations}
\label{sec:mathematics}

\subsection{Algorithm Complexity}
\label{ssec:complexity}

The time complexity of the primary algorithm is formalized as:

\begin{equation}
    T(n) = \sum_{i=1}^{k} c_i \cdot f_i(n) + O(n \log n)
    \label{eq:time-complexity}
\end{equation}

Where $c_i$ represents the cost coefficient for operation $i$ and $f_i(n)$ is the
complexity function of that operation.

For the recursive implementation:

\begin{equation}
    T(n) =
    \begin{cases}
        O(1) & \text{if } n \leq n_0 \\
        a \cdot T(n/b) + f(n) & \text{otherwise}
    \end{cases}
    \label{eq:recursive-complexity}
\end{equation}

Using the Master Theorem, this resolves to $T(n) = O(n^{\log_b a})$ when
$f(n) = O(n^{\log_b a - \epsilon})$.

\subsection{Data Flow Transformation}
\label{ssec:dataflow}

The data transformation pipeline can be represented as:

\begin{equation}
    \mathbf{Y} = \sigma(\mathbf{W} \cdot \mathbf{X} + \mathbf{b})
    \label{eq:linear-transformation}
\end{equation}

Where:
\begin{itemize}
    \item $\mathbf{X} \in \R^{n \times d}$ is the input matrix
    \item $\mathbf{W} \in \R^{d \times m}$ is the weight matrix
    \item $\mathbf{b} \in \R^{m}$ is the bias vector
    \item $\sigma$ is the activation function
\end{itemize}

The multi-stage transformation is:

\begin{equation}
    \mathbf{H}^{(l)} = \phi_l(\mathbf{W}^{(l)} \cdot \mathbf{H}^{(l-1)} + \mathbf{b}^{(l)})
    \label{eq:multi-layer}
\end{equation}

\subsection{State Machine Formalization}
\label{ssec:statemachine}

The system can be modeled as a deterministic finite automaton:

\begin{equation}
    M = (Q, \Sigma, \delta, q_0, F)
    \label{eq:automaton}
\end{equation}

Where:
\begin{itemize}
    \item $Q = \{q_0, q_1, q_2, \dots\}$ is the finite set of states
    \item $\Sigma = \{\text{event}_1, \text{event}_2, \dots\}$ is the input alphabet
    \item $\delta: Q \times \Sigma \rightarrow Q \times A$ is the transition function
    \item $q_0 \in Q$ is the initial state
    \item $F \subseteq Q$ is the set of accepting states
\end{itemize}

The transition function can be expanded as:

\begin{equation}
    \delta(q_i, e_j) =
    \begin{cases}
        (q_k, a_m) & \text{if } \exists \text{ transition} \\
        \text{undefined} & \text{otherwise}
    \end{cases}
    \label{eq:transition}
\end{equation}

\subsection{Neural Network Architecture (ML Models)}
\label{ssec:neural-architecture}

For deep learning models, the architecture is formalized:

\begin{equation}
    \mathcal{M} = (L, W, \phi, \theta)
    \label{eq:model-architecture}
\end{equation}

Where:
\begin{itemize}
    \item $L = \{l_1, l_2, \dots, l_K\}$ is the sequence of $K$ layers
    \item $W = \{\mathbf{W}^{(1)}, \mathbf{W}^{(2)}, \dots, \mathbf{W}^{(K)}\}$ are the weight matrices
    \item $\phi = \{\phi_1, \phi_2, \dots, \phi_K\}$ are the activation functions
    \item $\theta = \{\alpha, \beta, \gamma\}$ are hyperparameters
\end{itemize}

\subsubsection{Loss Function}

The primary loss function for classification:

\begin{equation}
    \mathcal{L}_{CE}(\theta) = -\sum_{i=1}^{N} y_i \log \hat{y}_i
    \label{eq:cross-entropy}
\end{equation}

For multi-task learning:

\begin{equation}
    \mathcal{L}_{total}(\theta) = \lambda_1 \mathcal{L}_{task1} + \lambda_2 \mathcal{L}_{task2} + \lambda_3 \mathcal{L}_{reg}
    \label{eq:multi-task-loss}
\end{equation}

Where regularization is:

\begin{equation}
    \mathcal{L}_{reg} = \lambda \|\mathbf{W}\|_F^2 + (1-\lambda) \sum_l \|\mathbf{W}^{(l)} - \mathbf{W}^{(l-1)}\|_F^2
    \label{eq:regularization}
\end{equation}

\subsubsection{Optimizer}

The Adam optimizer update rule:

\begin{equation}
    m_t = \beta_1 m_{t-1} + (1-\beta_1) g_t
    \label{eq:adam-momentum}
\end{equation}

\begin{equation}
    v_t = \beta_2 v_{t-1} + (1-\beta_2) g_t^2
    \label{eq:adam-velocity}
\end{equation}

\begin{equation}
    \theta_{t+1} = \theta_t - \frac{\alpha}{\sqrt{\hat{v}_t} + \epsilon} \hat{m}_t
    \label{eq:adam-update}
\end{equation}

Where $\hat{m}_t$ and $\hat{v}_t$ are bias-corrected estimates.

\subsection{Network Flow Model}
\label{ssec:network-flow}

For distributed systems:

\begin{equation}
    \text{Throughput} = \min_{s \in V} \sum_{e \in \delta^+(s)} f_e
    \label{eq:throughput}
\end{equation}

The latency model:

\begin{equation}
    L = \sum_{i=1}^{n} d_i + \sum_{i=1}^{n-1} p_i
    \label{eq:latency}
\end{equation}

Where $d_i$ is processing delay and $p_i$ is propagation delay.

\subsection{Probability Models}
\label{ssec:probability}

For uncertainty quantification:

\begin{equation}
    P(X | Y) = \frac{P(Y | X) \cdot P(X)}{P(Y)}
    \label{eq:bayes}
\end{equation}

Expectation calculation:

\begin{equation}
    \mathbb{E}[X] = \int_{-\infty}^{\infty} x \cdot f(x) dx
    \label{eq:expectation}
\end{equation}

\section{Figures and Diagrams}
\label{sec:figures}

\subsection{Architecture Diagram}
\input{figures/architecture.tex}

\subsection{Data Flow Diagram}
\input{figures/dataflow.tex}

\subsection{State Machine Diagram}
\input{figures/statemachine.tex}

\section{Tables}
\label{sec:tables}

\subsection{API Endpoints}
\input{tables/api-endpoints.tex}

\subsection{Module Dependencies}
\input{tables/module-deps.tex}
```

#### 5. figures/ — Diagram Generation

**architecture.tex:**
```latex
\begin{figure}[htbp]
  \centering
  \begin{tikzpicture}[node distance=2cm]
    % Use TikZ for architecture diagram
    \node[draw, rectangle] (client) {Client};
    \node[draw, rectangle, right of=client] (api) {API Gateway};
    \node[draw, rectangle, right of=api] (service) {Service};
    \node[draw, ellipse, below of=service] (db) {Database};

    \draw[->] (client) -- (api) node[midway, above] {HTTP};
    \draw[->] (api) -- (service);
    \draw[->] (service) -- (db);

    % Add more components as needed
  \end{tikzpicture}
  \caption{System Architecture}
  \label{fig:architecture}
\end{figure}
```

**statemachine.tex:**
```latex
\begin{figure}[htbp]
  \centering
  \begin{tikzpicture}[state/.style={circle, draw, minimum size=1.5cm}]
    \node[state, initial] (s0) {$q_0$};
    \node[state, right of=s0] (s1) {$q_1$};
    \node[state, right of=s1] (s2) {$q_2$};
    \node[state, accepting, right of=s2] (sf) {$q_f$};

    \draw[->] (s0) edge node[above] {$e_1$} (s1)
              (s1) edge node[above] {$e_2$} (s2)
              (s2) edge node[above] {$e_3$} (sf);
  \end{tikzpicture}
  \caption{State Machine Diagram}
  \label{fig:statemachine}
\end{figure}
```

#### 6. tables/ — Table Generation

**api-endpoints.tex:**
```latex
\begin{table}[htbp]
  \centering
  \caption{API Endpoint Summary}
  \begin{tabular}{|l|c|p{4cm}|l|}
    \hline
    \textbf{Endpoint} & \textbf{Method} & \textbf{Description} & \textbf{Auth} \\
    \hline
    /api/v1/users & GET & List all users & Bearer \\
    /api/v1/users & POST & Create user & Bearer \\
    /api/v1/users/\{id\} & GET & Get user by ID & Bearer \\
    /api/v1/users/\{id\} & PUT & Update user & Bearer \\
    /api/v1/users/\{id\} & DELETE & Delete user & Bearer \\
    \hline
  \end{tabular}
  \label{tab:api-endpoints}
\end{table}
```

#### 7. Makefile

```makefile
.PHONY: build clean view

LATEX = pdflatex
BIB = bibtex
MAIN = manuscript

build:
	$(LATEX) $(MAIN).tex
	$(BIB) $(MAIN)
	$(LATEX) $(MAIN).tex
	$(LATEX) $(MAIN).tex

clean:
	rm -f *.aux *.bbl *.blg *.log *.out *.toc *.lof *.lot *.fls *.fdb_latexmk

view: build
	open $(MAIN).pdf

# For draft mode (show boxes)
draft:
	$(LATEX) -draftmode $(MAIN).tex
	$(BIB) $(MAIN)
	$(LATEX) -draftmode $(MAIN).tex
	$(LATEX) $(MAIN).tex
```

## Manuscript Sections (Complete Structure)

### 1. Abstract
150-300 words summarizing:
- Problem statement
- Approach/methodology
- Key contributions
- Results/implications

### 2. Introduction
- Problem statement and motivation
- Research questions
- Contributions summary
- Paper structure overview

### 3. Background and Related Work
- Terminology and definitions
- Existing approaches in literature
- Comparison with related systems
- Gap analysis

### 4. System Architecture
- High-level design
- Component relationships
- Design patterns employed
- Architectural diagrams

### 5. Implementation Details
- Core algorithms with LaTeX equations
- Data structures
- Key abstractions
- Code examples (syntax highlighted)

### 6. Mathematical Foundations
- Algorithm complexity analysis
- Data flow transformations
- State machine formalization
- ML-specific: model architecture, loss functions, optimizers
- Network flow models

### 7. Performance Analysis
- Complexity analysis
- Scalability considerations
- Benchmark results

### 8. Discussion
- Strengths and limitations
- Comparison with state-of-the-art
- Practical implications

### 9. Conclusion and Future Work
- Summary of contributions
- Future research directions
- Open problems

### 10. References
- BibTeX formatted (both IEEE and ACM styles provided)

## Configuration Options

### Options
- `--depth` — Analysis level (shallow, medium, deep)
- `--format` — Citation style (ieee, acm, both)
- `--citations` — Include academic citations (default: true)
- `--equations` — Include mathematical formalization (default: true)
- `--figures` — Generate diagrams (default: true)
- `--ml` — Include ML-specific sections (auto-detected if ML project)
- `--cross-ref` — Cross-reference with wiki (default: true if exists)

## Quality Standards

1. **LaTeX compilation:** Must compile without errors
2. **Equations:** All LaTeX syntactically correct
3. **Citations:** Real academic refs + placeholders for user
4. **Figures:** TikZ/Mermaid code that renders correctly
5. **Tables:** Properly formatted with labels and captions
6. **Cross-references:** Accurate \ref{} and \cite{} usage
7. **Academic writing:** Formal, precise, no personal pronouns
8. **Security:** No secrets or .env values exposed
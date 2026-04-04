# Research Template

A GitHub template for academic research papers using LLM agents with rd-agent and adk-ralph.

## Overview

This template demonstrates a complete research workflow using:
- **rd-agent**: Microsoft R&D Agent for automated research
- **adk-ralph**: Multi-agent development for coding artifacts
- **ChromaDB**: Local vector embeddings
- **LangGraph**: Orchestration pipeline

## Quick Start

### 1. Create New Repository

Click "Use this template" above to create a new repository.

### 2. Clone and Setup

```bash
git clone https://github.com/YOUR_NAME/your-research-repo
cd your-research-repo

# Initialize submodules (if using agents as submodules)
git submodule update --init --recursive
```

### 3. Configure Environment

Copy `.env.example` to `.env` and configure:

```bash
cp .env.example .env
```

Edit `.env` with your settings:
```bash
CHAT_MODEL=ibm/granite-4-h-tiny
EMBEDDING_MODEL=text-embedding-nomic-embed-text-v1.5
LM_STUDIO_BASE_URL=http://localhost:1234/v1
```

### 4. Edit Paper Source

Edit files in `src/` directory (LaTeX format).

### 5. Automatic Builds

Push to trigger LaTeX → PDF compilation.

## Research Pipeline

### Phases

| Phase | Description | Agents |
|-------|-------------|--------|
| Questions | Extract questions from sources | rd-agent |
| Experiment | Design experiments | rd-agent + adk-ralph |
| Embeddings | Generate ChromaDB embeddings | LM Studio |
| Agent | Run agents (parallel) | rd-agent + adk-ralph |
| Results | Compile to JSON/LaTeX | Both |

### Running Phases

```bash
# Run specific phase
rd-agent-mcp run-phase questions
rd-agent-mcp run-phase experiment
rd-agent-mcp run-phase agent
rd-agent-mcp run-phase results

# Run full pipeline
rd-agent-mcp research-phase --topic "Your Topic"
```

## Test Cases

Test cases follow a YAML format inspired by GraphGameTreeTest:

```
test_cases/
├── CONFIG                      # Main config
├── rd_agent/
│   ├── q1/                   # Question 1
│   │   ├── CONFIG
│   │   ├── 0-survey.yaml
│   │   └── agents/
│   │       ├── rd-agent.yaml
│   │       └── adk-ralph.yaml
│   ├── q2/
│   └── q3/
```

### Running Tests

```bash
python -m rd_agent_mcp.test_runner --test-dir test_cases --question q1
```

## Homework Assignment (C S 4383/5388-001)

This template supports the Spring 2026 homework:

### Part 1: Survey Paper (q1)
- 6-8 pages, IEEE format
- Topic: Survey of Agentic Workflows in SE using LLM Agents

### Part 2: Reproduction Study (q2)
- Reproduce key finding from R&D-Agent paper
- Include JSON results and diagrams

### Part 3: Agentic Workflow Demo (q3)
Demonstrate using rd-agent and adk-ralph to produce:
- Python scripts with JSON output
- Rust CLI tools
- LaTeX tables and figures

## GitHub Actions

### Build PDF
Automatically compiles LaTeX on push to main.

### Research Pipeline
Run research phases manually:
1. Go to Actions tab
2. Select "Research Pipeline"
3. Choose phase and question
4. Click "Run workflow"

### Agent Demo
Demonstrates agent capabilities:
1. Python data analysis → JSON
2. Rust statistics tool → JSON
3. LaTeX table generation

## Agent Definitions

### rd-agent (Research Agent)
- Data analysis and processing
- ML model training
- Literature review
- Benchmark execution

### adk-ralph (Development Agent)
- Code generation (Rust, Python, etc.)
- Test-driven development
- CLI tool creation
- Multi-language support

## Directory Structure

```
.
├── .github/workflows/      # GitHub Actions
├── src/                   # LaTeX paper source
├── test_cases/           # YAML test cases
├── agents/               # Agent submodules
├── examples/             # Example code
├── output/               # Generated outputs
│   ├── results/
│   ├── embeddings/
│   └── diagrams/
└── README.md
```

## License

CC-BY 4.0 - See LICENSE file for details.

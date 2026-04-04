# rd-agent and adk-ralph Integration

This template uses two specialized agents for research and development tasks.

## rd-agent (Research Agent)

### Purpose
Automated research and data science tasks.

### Installation
```bash
cd agents
git clone https://github.com/sweeden-ttu/rd-agent
cd rd-agent
pip install -e .
```

### Usage
```bash
rdagent data_science --task "Analyze dataset for patterns"
rdagent general_model --paper "https://arxiv.org/abs/2505.14738"
```

### Capabilities
- Literature review and synthesis
- Data analysis and visualization
- ML model training and evaluation
- Benchmark execution
- Hypothesis generation

## adk-ralph (Development Agent)

### Purpose
Multi-agent code generation and system implementation.

### Installation
```bash
cd agents
git clone https://github.com/sweeden-ttu/adk-ralph
cd adk-ralph
cargo build --release
```

### Usage
```bash
# Full pipeline
cargo run -- "Create a CLI tool for data analysis"

# Interactive chat
cargo run -- chat
```

### Capabilities
- Rust, Python, TypeScript, Go, Java
- Test-driven development
- System architecture design
- PRD and design document generation
- Multi-agent orchestration

## Configuration

### Environment Variables

```bash
# rd-agent
RD_AGENT_MODEL=ibm/granite-4-h-tiny
RD_AGENT_PROVIDER=lm_studio
LM_STUDIO_BASE_URL=http://localhost:1234/v1

# adk-ralph
RALPH_MODEL_PROVIDER=ollama
RALPH_LOCAL_MODEL=granite4:3b
OLLAMA_HOST=http://localhost:11434
```

### Cloud Fallback

If local LLM is unavailable, agents fall back to cloud providers:

```bash
OPENAI_API_KEY=sk-...
ANTHROPIC_API_KEY=sk-ant-...
GEMINI_API_KEY=...
```

## Agent Routing

| Task Type | Primary Agent | Secondary Agent |
|-----------|---------------|-----------------|
| Data Analysis | rd-agent | adk-ralph |
| Literature Review | rd-agent | - |
| Code Generation | adk-ralph | rd-agent |
| Experiment Design | Both | - |
| Results Compilation | rd-agent | adk-ralph |

## Examples

### Python Data Analysis (rd-agent)
```python
rdagent data_science --task "Analyze MLE-Bench results"
# Output: results.json with metrics
```

### Rust CLI Tool (adk-ralph)
```bash
cargo run -- "Create a statistics CLI tool that outputs JSON"
# Output: bin/stat-cli, prd.md, design.md, tasks.json
```

### Combined Workflow
```bash
# 1. Generate analysis with rd-agent
rdagent data_science --task "Process survey data"

# 2. Create visualization tool with adk-ralph
cargo run -- "Create a Rust tool to generate charts from JSON"

# 3. Compile results
rd-agent-mcp compile-results --input output/
```

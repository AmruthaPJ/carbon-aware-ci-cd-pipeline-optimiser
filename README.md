# ⚡ CI/CD Optimiser — Carbon-Aware, Semantic & Graph-Aware Pipeline

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg?logo=python&logoColor=white)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.110%2B-009688.svg?logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.0%2B-EE4C2C.svg?logo=pytorch&logoColor=white)](https://pytorch.org/)
[![XGBoost](https://img.shields.io/badge/XGBoost-2.0%2B-orange.svg)](https://xgboost.readthedocs.io/)
[![HuggingFace](https://img.shields.io/badge/Model-CodeBERT%20%2F%20GraphCodeBERT-yellow.svg?logo=huggingface&logoColor=white)](https://huggingface.co/microsoft/codebert-base)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

An intelligent, next-generation CI/CD optimization system that eliminates compute waste and slashes carbon emissions. Instead of blindly executing every test suite on every pull request, this system analyzes code changes structurally and semantically, predicts failure probabilities with machine learning, and schedules regression workloads based on real-time electrical grid carbon intensity.

---

## 📑 Table of Contents

- [Overview](#-overview)
- [Why This Matters](#-why-this-matters)
- [System Architecture](#-system-architecture)
- [Key Features](#-key-features)
- [Visual Showcase (Dashboard)](#-visual-showcase)
- [Quick Start](#-quick-start)
  - [1. Installation](#1-installation)
  - [2. Quick Demo (Decision Engine & Mapper)](#2-quick-demo)
  - [3. Interactive Web Dashboard](#3-interactive-web-dashboard)
  - [4. Running on a Codebase / Git Diff](#4-running-locally-against-a-git-diff)
- [GitHub Actions CI/CD Integration](#-github-actions-cicd-integration)
- [Environment Variables & Configuration](#-environment-variables--configuration)
- [Repository File Map](#-repository-file-map)
- [License](#-license)

---

## 🌟 Overview

Modern software development teams run hundreds of CI/CD builds daily. Most runs redundantly execute unchanged integration or unit tests, consuming millions of CPU cycles and emitting significant CO₂ into dirty regional energy grids.

**GreenOps CI/CD Optimiser** brings intelligence and responsibility to pipeline execution by unifying:
1. **Structural AST parsing** & SHA-256 fingerprinting for rapid diff verification.
2. **Deep semantic code embeddings** via `microsoft/codebert-base` and `GraphCodeBERT`.
3. **Graph-based dependency analysis** (direct imports, reverse call trees, shared databases, and Kafka message buses).
4. **LLM impact reasoning** (Anthropic Claude, OpenAI, Google Gemini, or local Ollama).
5. **XGBoost gatekeeping** predicting failure probability ($P_f$) from 16 telemetry-driven features.
6. **Carbon-aware scheduling** querying live grid intensity APIs (Electricity Maps) and Ember global datasets.

---

## 📊 Why This Matters

| Metric / Concern | Traditional CI/CD | GreenOps CI/CD Optimiser |
| :--- | :--- | :--- |
| **Test Execution** | Runs entire test suite indiscriminately | Selects minimal high-signal tests relevant to PR changes |
| **Dependency Awareness** | Manual file globs or shallow syntax checks | Multi-tier: AST imports + semantic embeddings + Kafka/DB tracing |
| **Failure Prediction** | None (reactive failure) | Predictive: 16-feature XGBoost model predicts risk ($P_f$) |
| **Grid Awareness** | Runs immediately, ignoring grid carbon | Evaluates regional grid cleanliness; defers non-critical runs |
| **Compute Waste** | High developer wait time & unnecessary compute | 50%–80% reduction in redundant test execution cycles |
| **Carbon Impact** | Ignored | Actively measured, optimized, and minimized |

---

## 🧠 System Architecture

```
                  ┌──────────────────────────────────────────────┐
                  │           Pull Request / Git Diff            │
                  └──────────────────────┬───────────────────────┘
                                         │
                                         ▼
                  ┌──────────────────────────────────────────────┐
                  │ 1. AST Parser & SHA-256 Fingerprint Delta    │
                  └──────────────────────┬───────────────────────┘
                                         │
                                         ▼
                  ┌──────────────────────────────────────────────┐
                  │ 2. CodeBERT / GraphCodeBERT Embeddings       │
                  │    - Cosine similarity with stored modules   │
                  └──────────────────────┬───────────────────────┘
                                         │
                                         ▼
                  ┌──────────────────────────────────────────────┐
                  │ 3. Dependency Graph Construction             │
                  │    - Direct & reverse imports (Python/JS)    │
                  │    - Shared DB tables & Kafka bus topics     │
                  └──────────────────────┬───────────────────────┘
                                         │
                                         ▼
                  ┌──────────────────────────────────────────────┐
                  │ 4. LLM Impact Analyzer (Claude/Gemini/Ollama)│
                  │    - Structural reasoning & ripple effects   │
                  └──────────────────────┬───────────────────────┘
                                         │
                                         ▼
                  ┌──────────────────────────────────────────────┐
                  │ 5. XGBoost Gatekeeper Model                  │
                  │    - 16 feature signals → Failure Prob (Pf)  │
                  └──────────────────────┬───────────────────────┘
                                         │
                                         ▼
                  ┌──────────────────────────────────────────────┐
                  │ 6. Real-Time Carbon Intensity Engine         │
                  │    - Electricity Maps API / Ember fallback   │
                  │    - Evaluates clean vs. dirty grid window   │
                  └──────────────────────┬───────────────────────┘
                                         │
                                         ▼
                  ┌──────────────────────────────────────────────┐
                  │ 7. Test Selection & Pruning Strategy         │
                  │    - RUN high-signal tests                   │
                  │    - PRUNE safe tests / DEFER to clean grid  │
                  └──────────────────────┬───────────────────────┘
                                         │
                                         ▼
                  ┌──────────────────────────────────────────────┐
                  │ 8. CI/CD Orchestration & Reporting           │
                  │    - GitHub Actions runner & PR comment      │
                  │    - Real-time Web Dashboard                 │
                  └──────────────────────────────────────────────┘
```

---

## 🚀 Key Features

### 1. PR Fingerprinting & AST Structural Diffing
Converts each pull request into structural Abstract Syntax Trees (ASTs) and SHA-256 cryptographic fingerprints. If AST similarity against historical runs is high without logical divergence, existing dependency graphs are reused instantaneously.

### 2. Deep Semantic Code Embeddings
Uses `microsoft/codebert-base` (and GraphCodeBERT) to embed code at the module and function levels into dense vector spaces. Computes cosine similarities to uncover hidden, indirect dependencies that standard regex or syntax linters miss.

### 3. Comprehensive Dependency Graph Engine
Builds forward and reverse dependency maps across:
- **Language Imports**: Python (`ast`) and JavaScript/TypeScript import hierarchies.
- **Shared Databases**: Detects schemas and tables touched across modules.
- **Message Brokers**: Maps producers and consumers sharing Kafka topics.

### 4. LLM-Assisted Impact Analysis
Passes candidate graphs and diff semantics to LLMs (supports **Anthropic Claude**, **OpenAI**, **Google Gemini**, or free offline **Ollama**). The LLM reasons over the call chain, verifies ripple effects, and outputs a structured confidence risk assessment.

### 5. Failure-Aware Test Selection (XGBoost)
A production-grade XGBoost classifier evaluates 16 granular features:
- Embedding cosine similarity & change magnitude
- Direct vs. transitive graph depth
- Historical failure and flakiness rates
- Shared resource flags (DB, Kafka, network)
- Grid carbon intensity and AST hash mutation deltas

Tests with predicted failure probabilities ($P_f$) exceeding thresholds are prioritized; safe tests are pruned.

### 6. Carbon-Aware Workload Scheduling 🌱
- **Energy Estimation**: Estimates CPU cycle load and execution runtime for test suites.
- **Live Regional Carbon Telemetry**: Queries Electricity Maps (or regional Ember datasets) to detect whether data center runners are running on clean (hydro/wind/nuclear) or dirty (coal/thermal) grids.
- **Threshold Gating**: When grid carbon exceeds threshold (e.g., $> 500\text{ gCO}_2/\text{kWh}$), pruning thresholds tighten, and heavy non-critical regressions are scheduled for cleaner hours.

---

## 🖼 Visual Showcase

### Web Dashboard
Real-time overview of build status, carbon intensity, pruning metrics, and test recommendations.
![Dashboard](https://github.com/user-attachments/assets/10774ef5-0fda-4b5c-b3be-ed238f224947)

---

### Dependency Graph Visualizer
Interactive graph visualising direct imports, reverse dependents, and shared services.
![Dependencies](https://github.com/user-attachments/assets/bc91ba00-649b-41b9-a901-20a6e11a1bd3)

---

### Carbon Intensity Mapping
Live tracking of regional data center carbon footprints and clean-energy availability.
![Carbon intensity](https://github.com/user-attachments/assets/5264a4d9-779e-4ac3-a8fe-1ca19533568f)

---

### CI/CD Pruning Metrics
Breakdown of total discovered tests vs. selected vs. pruned tests with emission savings.
![CI/CD](https://github.com/user-attachments/assets/211ea38d-1ed5-467f-a0cb-c7c9bead80d5)

---

### LLM Explainability
Granular reasoning provided by LLMs for why specific tests were included or pruned.
![LLM explanation](https://github.com/user-attachments/assets/e9a724b9-c8c8-4e44-b7a0-ba2d17bfde98)

---

### GitHub Actions Integration
Automated PR checks, test matrix generation, and commit status comments.
![Integration with github actions](https://github.com/user-attachments/assets/2b3e7d50-ff59-41e4-bf62-38826bf91293)

---

## 🧪 Quick Start

### 1. Installation

Clone the repository and install required dependencies:

```bash
git clone https://github.com/akshaya209/Carbon-aware-ci-cd-pipeline-optimiser.git
cd Carbon-aware-ci-cd-pipeline-optimiser

# Recommended: create a virtual environment
python3 -m venv venv
source venv/bin/activate

# Install requirements
pip install -r requirements.txt
```

> **Note on PyTorch (CPU vs GPU)**: For fast, lightweight CPU execution in CI environments, install the CPU build:
> ```bash
> pip install torch --index-url https://download.pytorch.org/whl/cpu
> ```

---

### 2. Quick Demo

Run the standalone decision engine and step-by-step generative dependency mapper:

```bash
python3 main.py
```

Or simulate a complete test selection pipeline dry-run:

```bash
python3 pipeline_runner.py --demo
```

---

### 3. Interactive Web Dashboard

Launch the FastAPI-powered interactive web dashboard:

```bash
python3 dashboard/server.py
```

Open your browser and navigate to:
```
http://localhost:8000
```

From the dashboard, you can inspect dependency graphs, test execution decisions, regional carbon telemetry, and live LLM explanations.

---

### 4. Running Locally Against a Git Diff

You can run the optimizer directly on your current codebase:

```bash
# Step 1: Extract and cache embeddings for repository modules
python3 repo_module_extractor.py \
  --repo-root . \
  --repo-id your-org/your-repo \
  --output ./greenops_output

# Step 2: Build the import and dependency graph
python3 dependency_graph_engine.py \
  --repo-root . \
  --output ./greenops_output

# Step 3: Run the optimizer on your git diff
git diff main...HEAD > /tmp/pr.diff
python3 pipeline_runner.py \
  --repo your-org/your-repo \
  --diff /tmp/pr.diff \
  --output ./greenops_output
```

The output report will be generated at `./greenops_output/pipeline_report.json`.

---

## 🔄 GitHub Actions CI/CD Integration

GreenOps can be integrated directly into your GitHub Actions workflow using [action.yml](file:///Users/amrutha/Documents/Carbon-aware-ci-cd-pipeline-optimiser/action.yml).

### Example Workflow (`.github/workflows/carbon_ci.yml`)

```yaml
name: GreenOps Carbon-Aware CI

on:
  pull_request:
    types: [opened, synchronize, reopened]

jobs:
  optimize-and-test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v4
        with:
          fetch-depth: 0 # Full history required for diff computation

      - name: Setup Python
        uses: actions/setup-python@v5
        with:
          python-version: "3.11"
          cache: "pip"

      - name: Install Dependencies
        run: pip install -r requirements.txt

      - name: Run GreenOps Optimizer
        id: greenops
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          REPO_NAME: ${{ github.repository }}
          PR_NUMBER: ${{ github.event.pull_request.number }}
          ANTHROPIC_API_KEY: ${{ secrets.ANTHROPIC_API_KEY }} # Optional
          CO2SIGNAL_API_KEY: ${{ secrets.CO2SIGNAL_API_KEY }} # Optional
        run: |
          python3 greenops_integration.py

      - name: Run Selected Tests
        run: |
          # Read selected tests from output artifacts
          SELECTED_TESTS=$(cat greenops_output/selected_tests.txt 2>/dev/null || echo "tests/")
          pytest $SELECTED_TESTS
```

For more advanced multi-job workflows, error handling, and submodule sanitization, refer to the [INTEGRATION_GUIDE.md](file:///Users/amrutha/Documents/Carbon-aware-ci-cd-pipeline-optimiser/INTEGRATION_GUIDE.md).

---

## ⚙️ Environment Variables & Configuration

All components degrade gracefully when optional API keys are omitted.

| Variable | Default | Purpose |
| :--- | :--- | :--- |
| `GITHUB_TOKEN` | *None* | GitHub Personal Access Token or Actions token for PR diffs & status comments |
| `REPO_NAME` | *None* | Repository format (`owner/repo`) |
| `PR_NUMBER` | `0` | Pull Request number (`0` indicates local dry-run) |
| `CO2SIGNAL_API_KEY` | *None* | Electricity Maps API key for live grid carbon intensity. *(Falls back to Ember 2024 regional averages if omitted)* |
| `GREENOPS_CARBON_THRESHOLD` | `500` | Grid carbon threshold in $\text{gCO}_2/\text{kWh}$ above which strict pruning applies |
| `PF_THRESHOLD` | `0.30` | Minimum predicted failure probability ($P_f$) required to execute a test candidate |
| `GREENOPS_CONFIDENCE_MIN` | `0.60` | Safety threshold: if pruner confidence is low, falls back to full test run |
| `ANTHROPIC_API_KEY` | *None* | Anthropic API key for Claude LLM impact analysis |
| `GEMINI_API_KEY` | *None* | Google Gemini API key fallback for LLM impact analysis |
| `OPENAI_API_KEY` | *None* | OpenAI API key fallback for LLM impact analysis |
| `OLLAMA_BASE_URL` | `http://localhost:11434` | Local Ollama endpoint for free, local offline LLM reasoning |
| `GREENOPS_OUTPUT` | `./greenops_output` | Directory where output graphs, models, and reports are written |
| `GREENOPS_DB_PATH` | `./greenops_output/module_registry.sqlite` | SQLite database storing file embeddings and SHA-256 hashes |
| `GREENOPS_S3_BUCKET` | *None* | Optional AWS S3 bucket to persist the embedding database across ephemeral CI runners |

---

## 📂 Repository File Map

```
Carbon-aware-ci-cd-pipeline-optimiser/
├── action.yml                     # Reusable GitHub Action specification
├── main.py                        # Standalone demo entry point for engine & mapper
├── pipeline_runner.py             # CLI runner for diff evaluation & simulation
├── greenops_integration.py        # Complete 8-stage orchestrator for GitHub Actions
├── requirements.txt               # Project dependencies
├── INTEGRATION_GUIDE.md           # In-depth architectural & deployment guide
├── dashboard/                     # Web Dashboard Application
│   ├── server.py                  # FastAPI server with REST endpoints & uvicorn runner
│   ├── static/                    # CSS stylesheets, JavaScript client, and assets
│   └── templates/                 # Dashboard HTML templates
├── src/                           # Core logic modules
│   ├── core/
│   │   └── decision_engine.py     # Carbon-aware test pruning decision matrix
│   ├── ml/
│   │   └── gatekeeper.py          # XGBoost failure probability prediction
│   ├── ai/
│   │   └── llm_agent.py           # Multi-provider LLM caller (Claude, GPT, Ollama)
│   └── config/
│       └── settings.py            # Global settings & default thresholds
├── ast_parser.py                  # Python & Java AST parsing utilities
├── repo_module_extractor.py       # CodeBERT module embedding generator & SQLite store
├── dependency_graph_engine.py     # Import parser, reverse graph builder & test mapper
├── pr_diff_processor.py           # Git diff parser, embedding comparator & AST deltas
├── xgboost_gatekeeper.py          # 16-feature XGBoost model trainer & inferencer
├── llm_impact_analyzer.py         # LLM ripple effect analysis & impact scoring
├── test_selection_engine.py       # Signal aggregator producing final test candidate list
├── carbon_inference_engine.py     # Regional live grid carbon & Ember dataset client
├── carbon_aware_scheduler.py      # Multi-region carbon-aware workload scheduler
├── module_embedding_store.py      # SQLite / S3 persistent embedding repository
└── preprocessing.py               # Pre-submit and post-submit telemetry data processor
```

---

## 📜 License

This project is open-source under the [MIT License](LICENSE).
Feel free to use, modify, and distribute it in your own pipelines.

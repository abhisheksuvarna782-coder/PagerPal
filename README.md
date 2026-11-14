⚡ PAGERPAL

Autonomous Multi-Agent Incident Response Console

From incident detection to evidence-backed resolution — intelligently, safely, and autonomously.

<p align="center">Built for AgentX | SYNERGY | Sahyadri College of Engineering and Management

</p><p align="center">
  <img src="https://img.shields.io/badge/AI-Multi--Agent%20System-8B5CF6?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Orchestration-LangGraph-2563EB?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Backend-FastAPI-009688?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Frontend-React-61DAFB?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Visualization-Three.js-black?style=for-the-badge" />
</p><p align="center">
  <a href="https://pagerpal.vercel.app/">🌐 Live Demo</a> •
  <a href="#-features">Features</a> •
  <a href="#-architecture">Architecture</a> •
  <a href="#-project-structure">Project Structure</a> •
  <a href="#-getting-started">Getting Started</a> •
  <a href="#-team">Team</a>
</p>---

🚨 The Problem

Modern software systems operate through interconnected services, databases, APIs, and infrastructure components.

When something breaks, engineers often need to:

- Investigate multiple monitoring dashboards.
- Correlate alerts, logs, metrics, and traces.
- Identify the actual root cause.
- Understand the impact on downstream services.
- Decide which remediation action is safe.
- Verify whether the system has recovered.

This process can consume valuable time, especially during critical incidents.

💡 Our Solution — PagerPal

PagerPal is an evidence-driven, safety-controlled autonomous incident response platform powered by a multi-agent AI architecture.

It transforms traditional incident management into an intelligent workflow where specialized AI agents collaborate to investigate incidents, identify root causes, evaluate risks, and recommend safe remediation actions.

Unlike conventional AI automation tools, PagerPal separates AI decision-making from execution permissions through an independent Python-based policy engine.

Our Vision

«Turn a 30-minute, 3 AM incident-response scramble into a 2-minute, evidence-backed approve-and-resolve workflow.»

🌐 Live Application: https://pagerpal.vercel.app/

---

✨ Features

1. Multi-Agent AI Investigation

PagerPal uses LangGraph to coordinate specialized agents through a structured incident-response workflow.

Agent| Responsibility
Supervisor Agent| Controls workflow execution and agent coordination
Triage Agent| Evaluates incident severity and blast radius
Investigator Agent| Examines logs, metrics, traces, and deployments
Causal RCA Engine| Identifies probable root causes through dependency graphs
Evidence Verifier| Validates investigation claims against telemetry
Confidence Scorer| Calculates deterministic confidence scores
Remediation Agent| Recommends approved recovery actions
Communications Agent| Generates notifications and incident postmortems

2. Causal Root Cause Analysis

Powered by NetworkX, PagerPal models service dependencies as a directed graph.

It helps identify:

- Probable root causes.
- Upstream and downstream dependencies.
- Causal paths between affected services.
- Counterfactual checks.
- Potential blast radius.

3. Evidence-Based Verification

PagerPal does not blindly trust AI-generated conclusions.

Investigation claims are checked against empirical telemetry. Unsupported claims are rejected through bounded verification and retry mechanisms.

4. Independent Safety Policy Engine

A dedicated Python policy engine controls what the system is allowed to execute.

- L1: Safe diagnostic operations.
- L2: Approved, reversible remediation actions.
- L3: High-risk actions requiring escalation.

The LLM cannot override the policy engine.

5. Human-in-the-Loop Approval

Remediation is not automatically executed just because an AI agent recommends it.

A mandatory human approval checkpoint is enforced through LangGraph interrupts.

The operator can review, approve, or reject the proposed action.

6. Independent Recovery Verification

After an approved remediation, PagerPal compares before-and-after system metrics.

Recovery checks include:

- P95 latency.
- Error rates.
- Synthetic health probes.

If recovery verification fails, the incident is escalated instead of being incorrectly marked as resolved.

7. Incident Knowledge Base

An SQLite-powered knowledge base stores historical incidents, summaries, and runbooks.

Previous incidents can provide suggestions, but historical fixes are never automatically executed.

8. External Integrations

- GitHub API integration for recent commit investigation.
- Slack and Discord webhook notifications.
- Retry mechanisms with backoff.
- Transparent mock fallbacks when external integrations are unavailable.

---

🧠 What Makes PagerPal Different?

PagerPal combines agentic intelligence, causal analysis, deterministic safety enforcement, and human accountability.

Traditional Monitoring| PagerPal
Displays alerts| Investigates incidents
Requires manual correlation| Correlates telemetry
Relies on manual RCA| Uses causal dependency analysis
Human manually researches fixes| AI proposes evidence-backed remediation
Automation executes predefined actions| Independent policy engine controls execution
Assumes action success| Independently verifies recovery

The key innovation is not simply using AI to fix incidents. It is combining agentic intelligence with deterministic safety enforcement and human accountability.

---

🏗️ Architecture

PagerPal follows a modular multi-agent architecture designed to separate investigation, decision-making, safety validation, execution, and recovery verification.

High-Level Agent Workflow

flowchart TD
    A["Simulated Monitoring Telemetry"] --> B["Supervisor Agent"]
    B --> C["Triage Agent"]
    C --> D["Investigator Agent"]
    D --> E["Causal RCA Engine"]
    E --> F["Evidence Verifier"]
    F --> G["Confidence Scorer"]
    G --> H["Remediation Agent"]
    H --> I["Independent Python Policy Engine"]
    I --> J{"Human Approval"}
    J -->|Approved| K["Execute Remediation"]
    J -->|Rejected| L["Stop / Escalate"]
    K --> M["Recovery Verification"]
    M --> N{"Recovery Successful?"}
    N -->|Yes| O["Resolve Incident"]
    N -->|No| L
    O --> P["Knowledge Base & Postmortem"]

System Architecture

The platform consists of interconnected layers responsible for user interaction, API communication, agent orchestration, safety enforcement, persistence, and integrations.

flowchart TB
    U["Operator / User"]
    
    subgraph FRONTEND["Presentation Layer"]
        UI["React Dashboard"]
        V["Three.js 3D Topology"]
    end

    subgraph BACKEND["Backend Layer"]
        API["FastAPI Backend"]
    end

    subgraph INTELLIGENCE["Agentic Intelligence Layer"]
        S["Supervisor Agent"]
        T["Triage Agent"]
        I["Investigator Agent"]
        RCA["NetworkX Causal RCA"]
        E["Evidence Verifier"]
        C["Confidence Scorer"]
        R["Remediation Agent"]
        COM["Communications Agent"]
    end

    subgraph SAFETY["Safety & Execution Layer"]
        P["Python Policy Engine"]
        H["Human Approval Gate"]
        X["Controlled Remediation"]
        RV["Recovery Verification"]
    end

    DB[("SQLite Database")]
    EXT["GitHub / Slack / Discord"]

    U --> UI
    UI --> V
    UI <--> API
    API <--> S
    S --> T --> I --> RCA --> E --> C --> R
    R --> P --> H
    H -->|Approved| X
    H -->|Rejected| API
    X --> RV
    RV --> DB
    COM --> EXT
    API <--> DB

Architecture Layers

Layer| Technology| Responsibility
Presentation| React, Three.js| Interactive dashboard and 3D infrastructure visualization
API| FastAPI| Backend endpoints and application communication
Orchestration| LangGraph| Agent coordination and workflow management
Intelligence| Claude, NetworkX| AI reasoning, investigation, and causal analysis
Safety| Python Policy Engine| Permission validation and execution restrictions
Approval| Human-in-the-Loop| Operator authorization
Recovery| Recovery Verifier| Before-and-after metric validation
Persistence| SQLite| Incidents, audit logs, and knowledge base
Integrations| GitHub, Slack, Discord| External investigation and notifications

Incident Processing Lifecycle

1. Detection: Simulated monitoring telemetry generates an incident.
2. Triage: The system evaluates severity and potential blast radius.
3. Investigation: Agents collect and correlate diagnostic evidence.
4. Root Cause Analysis: NetworkX evaluates service dependencies and causal paths.
5. Verification: Investigation claims are validated against telemetry.
6. Decision: A deterministic confidence score is calculated.
7. Safety Validation: The Python policy engine checks the proposed remediation.
8. Human Approval: The operator approves or rejects the action.
9. Execution: Approved remediation is executed.
10. Recovery: Independent verification checks whether the system recovered.
11. Documentation: Incident details and postmortems are persisted.

Core Architecture Principles

1. Separation of Intelligence and Authority: AI agents investigate and recommend; the policy engine controls execution permissions.
2. Evidence Before Action: Remediation recommendations must be supported by verified evidence.
3. Human Accountability: Mandatory approval before remediation execution.
4. Verified Recovery: An incident is resolved only after independent recovery checks.
5. Auditable Execution: Incident decisions and actions are recorded.

---

📁 Project Structure

PagerPal follows a modular project structure that separates backend services, agent orchestration, frontend visualization, testing, evaluation, and deployment.

PagerPal/
│
├── backend/
│   │
│   ├── main.py
│   │
│   ├── agents/
│   │   ├── supervisor.py
│   │   ├── triage.py
│   │   ├── investigator.py
│   │   ├── remediation.py
│   │   └── communications.py
│   │
│   ├── tests/
│   │   ├── test_stage_a_simulator.py
│   │   ├── test_stage_b_correlation_rca.py
│   │   ├── test_stage_c_verifier_policy.py
│   │   ├── test_stage_d_workflow.py
│   │   ├── test_stage_e_kb_postmortem.py
│   │   └── test_backend.py
│   │
│   └── eval/
│       └── run_eval.py
│
├── frontend/
│   │
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── assets/
│   │   └── ...
│   │
│   ├── public/
│   ├── package.json
│   ├── vite.config.js
│   └── vercel.json
│
├── eval_results/
│   ├── eval_results.csv
│   └── eval_summary.md
│
├── run.py
├── render.yaml
├── requirements.txt
├── DEPLOYMENT.md
├── DEMO.md
└── README.md

Note: This is an illustrative logical structure. Verify actual filenames and folders against the repository before publishing.

Core Module Responsibilities

Module| Purpose
"backend/main.py"| FastAPI application entry point
"backend/agents/"| Specialized AI agent implementations
"backend/tests/"| Automated unit and integration tests
"backend/eval/"| Incident evaluation benchmark
"frontend/src/"| React dashboard and visualization components
"eval_results/"| Benchmark reports and evaluation results
"run.py"| Application startup
"render.yaml"| Backend deployment configuration
"DEPLOYMENT.md"| Deployment instructions
"DEMO.md"| Demonstration walkthrough

---

🛠️ Technology Stack

PagerPal combines agentic AI, graph-based causal analysis, deterministic policy enforcement, and immersive infrastructure visualization.

AI & Intelligence Layer

Technology| Purpose
LangGraph| Multi-agent orchestration and workflow state management
Claude| Structured AI reasoning and tool calling
NetworkX| Service dependency graphs and causal RCA
Python Policy Engine| Independent safety validation
Deterministic Confidence Scorer| Rule-based confidence calculation

Backend & Data Layer

Technology| Purpose
Python 3.11+| Core backend development
FastAPI| REST API and backend services
Uvicorn| ASGI server
SQLite| Incident and knowledge persistence
Pytest| Automated testing

Frontend & Visualization Layer

Technology| Purpose
React 18| Interactive frontend
Vite| Development and build tooling
Three.js| 3D infrastructure topology visualization
Sora Typography| Visual identity and interface typography

Deployment & Integrations

Technology| Purpose
Vercel| Frontend deployment
Render| Backend deployment
GitHub API| Repository and commit investigation
Slack / Discord Webhooks| Incident notifications

---

🔐 Safety & Security

PagerPal is designed around controlled autonomy.

- All monitoring telemetry is simulated and labelled "SIMULATION".
- No real customer or financial data is processed by the simulator.
- Diagnostic tools operate through allowlisted, read-only interfaces.
- Untrusted telemetry is sanitized and isolated.
- Remediation actions must match an exact policy allowlist.
- High-risk actions are restricted and escalated.
- Human approval is mandatory before remediation execution.
- Recovery must be independently verified.
- Historical knowledge-base fixes remain suggestions only.

Our Safety Philosophy

AI proposes. Policy validates. Humans authorize. Recovery verification confirms.

---

📊 Testing & Evaluation

PagerPal includes an automated testing and evaluation framework covering the major stages of the incident-response workflow.

Automated Test Suite

Run:

python -m pytest backend/tests/ -v

53 automated tests across five development stages and backend validation.

Test Suite| Coverage
Stage A — Simulator| Fault simulation, reproducibility, ground-truth isolation
Stage B — Correlation & RCA| Alert correlation, causal ranking, missing telemetry
Stage C — Verification & Policy| Evidence validation, confidence scoring, policy enforcement, prompt injection
Stage D — Workflow| End-to-end orchestration, approval/rejection, recovery failure, emergency stop
Stage E — Knowledge Base| SQLite persistence, suggestions, postmortems
Backend Tests| API endpoints, dashboard KPIs, evaluation harness

Evaluation Benchmark

PagerPal supports an automated benchmark across 12 incident scenarios.

Run:

python -m backend.eval.run_eval

Results are generated in:

eval_results/
├── eval_results.csv
└── eval_summary.md

---

🚀 Getting Started

Prerequisites

- Python 3.11 or later.
- Node.js and npm.
- Git.
- Claude API key for AI-powered functionality.

1. Clone the Repository

git clone <YOUR_GITHUB_REPOSITORY_URL>
cd PagerPal

2. Configure Environment Variables

Create the required environment configuration using the project's supported settings.

Example:

ANTHROPIC_API_KEY=your_api_key

Configure optional GitHub and notification webhook credentials when required.

Never commit API keys or secrets to GitHub.

3. Install Backend Dependencies

pip install -r requirements.txt

4. Install Frontend Dependencies

cd frontend
npm install
cd ..

5. Run the Application

python run.py

Open:

http://localhost:8000

API documentation:

http://localhost:8000/docs

Development Mode

Terminal 1 — Backend

python -m uvicorn backend.main:app --port 8000 --reload

Terminal 2 — Frontend

cd frontend
npm run dev

Open:

http://localhost:5173

---

☁️ Deployment

PagerPal uses a separated frontend and backend deployment architecture.

Component| Platform
Frontend| Vercel
Backend| Render
Database| SQLite

Deployment Configuration

vercel.json
render.yaml
DEPLOYMENT.md

For complete deployment instructions, refer to "DEPLOYMENT.md".

Live Deployment

🌐 Frontend: https://pagerpal.vercel.app/

---

🎬 Live Demonstration

Explore PagerPal through the deployed application.

🌐 Demo: https://pagerpal.vercel.app/

Demonstration Workflow

1. Incident detection and triage.
2. Multi-agent investigation.
3. Causal root cause analysis.
4. Evidence verification and confidence scoring.
5. Remediation recommendation.
6. Human approval and policy enforcement.
7. Recovery verification.
8. Incident reporting and postmortem generation.

For the complete demonstration flow, refer to "DEMO.md".

---

👥 Team

Built by Team PagerPal

Developed for AgentX at SYNERGY, Sahyadri College of Engineering and Management.

Team Member
Ajiras Abhishek
Ajay Raj A M
Rishitha R
Rithu

---

🎯 Our Vision

We believe the future of incident management is not just automated monitoring.

It is intelligent systems that can understand failures, investigate evidence, reason about dependencies, recommend safe actions, and verify outcomes — without compromising human control.

PagerPal brings autonomous intelligence and responsible automation together.

---

<p align="center">⚡ PAGERPAL

Investigate Smarter. Respond Faster. Recover Safely.

Built for AgentX | SYNERGY | Sahyadri College of Engineering and Management

</p>

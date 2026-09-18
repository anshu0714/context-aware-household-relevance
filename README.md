# Context-Aware Household Relevance

**ContextLens** — *See who a household record is relevant to.*

A research prototype for studying whether structured household context improves an AI system's ability to infer the relevance of personal electronic records to household members.

> **This is an academic research prototype, not a document-management or automatic-sharing system.**

## Research Question

> How accurately can an AI system infer the household relevance of personal electronic records using document content and household context?

## Experiment

The project compares two conditions using the **same scenarios and test set**:

| Condition | AI Input |
|---|---|
| **A — Document Only** | Document content |
| **B — Document + Context** | Document content + structured household context |

Both conditions produce the same structured prediction format and are compared against independently created ground truth.

```text
                 Same Scenario
                      │
             ┌────────┴────────┐
             ▼                 ▼
      Document Only     Document + Context
          (A)                  (B)
             │                 │
             ▼                 ▼
          AI Model          AI Model
             │                 │
             └────────┬────────┘
                      ▼
                 Ground Truth
                      │
                      ▼
              Metrics + Errors
```

## Relevance Classes

- `PERSONAL` — primarily relevant to one member
- `HOUSEHOLD_WIDE` — relevant to most/all members
- `SELECTIVE` — relevant to specific members
- `UNCERTAIN` — insufficient evidence for a reliable decision

## Evaluation

The experiment measures:

- Classification accuracy
- Recipient precision
- Recipient recall
- Recipient F1-score
- Unnecessary-sharing rate
- Uncertainty / abstention rate
- Error patterns

Error analysis covers false recipients, missed recipients, wrong classes, unsupported inference, over-sharing, under-sharing, and uncertain-case failures.

## Scope

### Included

- Synthetic household profiles and documents
- PDF/text extraction
- Structured household context
- AI relevance inference
- Condition A and Condition B comparison
- Automated evaluation
- Error analysis
- Minimal web prototype

### Excluded

- Real personal/financial documents
- Automatic document sharing
- Full household account management
- Mobile application
- Multi-agent systems
- Custom ML model training
- Large-scale document crawling
- Complex RBAC
- Production deployment

## Technology Stack

- **Frontend:** React + Vite
- **Backend:** Node.js + Express
- **Document Processing:** Open-source PDF/text extraction
- **AI:** Local/open model where practical
- **Data:** JSON / SQLite / MongoDB
- **Evaluation:** Python
- **Version Control:** Git

The project prioritizes free/open-source tools and keeps infrastructure minimal.

## Project Structure

```text
context-aware-household-relevance/
├── backend/
├── frontend/
├── dataset/
│   ├── documents/
│   ├── households.json
│   └── ground-truth.json
├── evaluation/
│   ├── evaluate.py
│   ├── metrics.py
│   └── results/
├── docs/
│   ├── architecture.md
│   ├── experiment.md
│   └── screenshots/
├── .gitignore
└── README.md
```

## Prototype

**ContextLens** provides a minimal interface to:

1. Select/upload a synthetic document.
2. Select or view household context.
3. Run Condition A and/or Condition B.
4. View predicted relevance and recipients.
5. Compare both conditions.
6. Inspect evaluation results.

The UI is intentionally secondary to the research experiment.

## Research Integrity

- Ground truth is created independently of AI predictions.
- The same final test set is used for both conditions.
- Raw predictions are preserved.
- Predictions are not manually corrected before evaluation.
- Difficult cases are not removed because of poor results.
- The final test set is frozen before the main experiment.
- Results are reported only after the actual experiment.
- Negative or inconclusive findings are reported honestly.

## Status

**Current Phase:** Phase 0 — Project Setup

Implementation follows the defined execution plan:

```text
Phase 0  → Project Setup
Phase 1  → Dataset + Ground Truth
Phase 2  → Synthetic Documents
Phase 3  → Backend + Extraction
Phase 4  → Condition A + B AI Inference
Phase 5  → Minimal Web Prototype
Phase 6  → Evaluation Pipeline
Phase 7  → Error Analysis
Phase 8  → Reproducibility
Phase 9  → Results + Visuals
Phase 10 → Research Paper Update
Phase 11 → Technical Documentation
Phase 12 → Final Testing + Submission
```

## Quick Start

> Setup and run instructions will be added as the implementation is completed.

---

**Academic Project:** MCA Minor Project  
**Repository:** `context-aware-household-relevance`  
**Prototype:** `ContextLens`

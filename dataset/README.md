# Dataset

This directory contains the synthetic dataset used for the
Context-Aware Household Relevance research experiment.

## Research Purpose

The dataset is used to investigate whether structured household
context improves an AI system's ability to:

1. Classify the relevance of a personal electronic record.
2. Identify the household members for whom the record is relevant.

The experiment compares two conditions:

### Condition A — Document Only

The AI receives only the extracted document text.

### Condition B — Document + Household Context

The AI receives the same extracted document text together with
structured information about the relevant household and its members.

The same scenario must be evaluated under both conditions.

---

## Dataset Files

### `households.json`

Contains synthetic household profiles.

Each household contains:

- `household_id`
- `member_id`
- synthetic display name
- household role
- relevant responsibilities

Only information relevant to household document relevance is included.

No real personal information is used.

### `scenarios.json`

Contains the document scenario definitions.

Each scenario includes:

- scenario ID
- household ID
- document category
- document type
- document description
- document owner metadata
- dataset split
- provisional ambiguity level
- leakage review status

Ground-truth answers are intentionally NOT stored in this file.

### `ground-truth.json`

Contains the independently created research ground truth.

For every scenario it specifies:

- relevance class
- correct recipient/member set
- ground-truth reasoning

Ground truth must be created independently of AI predictions.

---

## Relevance Classes

The experiment uses four relevance classes.

### PERSONAL

The document is primarily relevant to one household member.

Example:

An individual salary statement.

### HOUSEHOLD_WIDE

The document is relevant to most or all members of the household.

Example:

A shared household electricity bill.

### SELECTIVE

The document is relevant to specific household members.

Example:

A school document concerning one student and the parent responsible
for school administration.

### UNCERTAIN

The available information is insufficient to reliably determine
the relevant household member or members.

The AI is allowed to abstain using the `UNCERTAIN` class rather than
being forced to select a recipient.

---

## Ground Truth Rules

Ground truth is created independently before AI evaluation.

The AI prediction pipeline must never receive:

- ground-truth relevance classes
- ground-truth recipient lists
- ground-truth reasons
- evaluation metrics
- expected outputs

Ground truth is used only after prediction to calculate evaluation
metrics.

---

## Owner Metadata

`owner_member_id` identifies the synthetic document owner during
dataset construction.

It is dataset metadata and must NOT automatically be provided to
the AI model.

If the document itself identifies a person, that information may
naturally appear in the extracted document text.

This distinction prevents the experiment from trivially giving the
model the answer.

---

## Dataset Splitting

The initial ten scenarios are development scenarios.

They are intended for:

- pipeline testing
- schema validation
- document-generation testing
- prompt/procedure development
- debugging

They are not the final evaluation dataset.

The final evaluation dataset will be created separately and frozen
before the main experiment.

The final test set must not be modified after evaluation begins.

---

## Leakage Prevention

The following rules apply:

1. Ground truth must not be generated from AI predictions.
2. Ground-truth files must not be supplied to the inference system.
3. Final evaluation examples must not be used for prompt tuning.
4. Development and final evaluation scenarios must remain separate.
5. The final evaluation dataset must be frozen before the main run.
6. Difficult scenarios must not be removed merely because they reduce
   model performance.
7. AI predictions must not be manually edited before evaluation.

---

## Synthetic Data and Privacy

All households and documents are synthetic.

The dataset must not contain:

- real identity documents
- real financial records
- real medical records
- real educational records
- real addresses
- real account numbers
- real government identifiers
- real personal contact information

The purpose of synthetic data is to allow controlled evaluation
without collecting sensitive household records.

---

## Current Dataset Status

Phase 1 currently contains:

- 4 synthetic households
- 13 synthetic household members
- 10 development scenarios
- independently defined ground truth

The ten scenarios cover:

- Utilities
- Education
- Insurance
- Employment
- Warranties/Receipts
- Travel
- Property/Rental

The dataset will later be expanded to approximately 80 scenarios
across the planned document categories.

---

## Experimental Integrity

The same scenario must be used for both conditions.

Condition A:

Document → AI → Prediction

Condition B:

Document + Household Context → AI → Prediction

The predictions are evaluated against the same independently
created ground truth.

No automatic document sharing occurs.

The system only produces relevance and recipient recommendations
for research evaluation.

---

## Phase 1 Review Status

The initial dataset is ready for ambiguity and leakage review.

The `ambiguity_level` and `leakage_review` fields in `scenarios.json`
are provisional until the review is completed.

After review, the ten development scenarios can be used for
pipeline validation before expanding the dataset.

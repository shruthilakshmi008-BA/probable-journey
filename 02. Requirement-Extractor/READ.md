# Module 02: AI-Assisted Stakeholder Discovery & Requirements Extractor

## Executive Summary
Stakeholder discovery sessions, call transcripts, and email threads contain unstructured, highly conversational feedback. This module automates the extraction and categorization of raw stakeholder commentary into structured Business Requirements Document (BRD) artifacts, classifying requirements by functional type and operational priority.

---

## Business Problem & Efficiency Gains
* **Problem Statement:** Manual conversion of raw stakeholder meeting notes into structured requirement statements takes 2–4 hours per session and suffers from human bias in priority assignment.
* **Business Value:** Cuts discovery-to-documentation cycle times by ~75%, standardization of functional vs. non-functional requirements taxonomy, and eliminates transcript filler language.

---

## Requirements Mapping Taxonomy

Raw conversational input is parsed and transformed into a formal requirements matrix:

| Field | Description | Target Values |
| :--- | :--- | :--- |
| `requirement_id` | Unique traceable identifier | `REQ-001`, `REQ-002`, etc. |
| `description` | Formatted requirement statement | Stripped of conversational filler (e.g., *"So basically..."*) |
| `type` | Architectural categorization | `Functional` / `Non-Functional` |
| `priority` | Urgency heuristic based on business language | `High` / `Medium` / `Low` |

---

## Example Extraction Output

### Raw Stakeholder Input:
> *"So basically the biggest issue right now is that when a purchase request comes in from a branch, nobody knows who's supposed to approve it if it's over 50k..."*

### Transformed Requirements Output Table:

| requirement_id | description | type | priority | source_extraction_method |
| :--- | :--- | :--- | :--- | :--- |
| `REQ-001` | Establish approval hierarchy for branch purchase requests exceeding $50k. | Functional | High | OpenAI GPT-4o-mini |
| `REQ-002` | Require vendor quote attachments prior to purchase request submission. | Functional | High | OpenAI GPT-4o-mini |
| `REQ-003` | Automated notification reminders for pending approval requests. | Functional | Medium | OpenAI GPT-4o-mini |
| `REQ-004` | Approval workflow execution within a maximum 3 business day SLA. | Non-Functional | High | OpenAI GPT-4o-mini |
| `REQ-005` | Finance portal dashboard displaying real-time pending request status. | Functional | Low | OpenAI GPT-4o-mini |

---

## Directory Structure
```text
02-Requirements-Extractor/
 ├── requirements_extractor.py  # Core Extraction Pipeline
 ├── stakeholder_notes.txt      # Input Raw Discovery Transcript
 └── requirements_output.csv    # Exported Requirements Matrix

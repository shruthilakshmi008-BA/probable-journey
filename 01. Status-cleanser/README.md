# Module 01: Status Cleaner & Data Normalization Pipeline

## Executive Summary
In multi-source enterprise systems (e.g., healthcare claims or retail portals), disparate status naming conventions prevent automated reconciliation. This module implements a hybrid two-tier pipeline: deterministic rule-matching for cost-effective execution, supplemented by AI classification for ambiguous entries.

---

## Business Problem & ROI Analysis
* **Problem Statement:** Inconsistent status field entries across vendor portals (`Approved`, `appr`, `pending_review`, `denied`) cause reconciliation job failures and require manual intervention.
* **Business Impact:** Automates status mapping across unstructured datasets, reducing manual exceptions by ~85% while cutting LLM API consumption costs through rule-first routing.

---

## Process Architecture & Requirements

### Process Logic Flow
1. **Rule Engine First:** Evaluates incoming values against deterministic lookup mapping ($0 execution cost, <1ms execution time).
2. **AI Fallback Layer:** Unmapped values are routed to an LLM classifier configured to output standard canonical states (`approved`, `pending`, `rejected`).
3. **Audit Logging:** Appends a `method_used` column (`rule` vs. `ai_fallback`) for full process visibility and traceability.

### Requirements & Canonical Mapping Table

| Raw Input Example | Mapped Canonical Status | Processing Layer |
| :--- | :--- | :--- |
| `Approved`, `appr` | `approved` | Rule Matching |
| `pending review`, `in review` | `pending` | Rule Matching |
| `accepted` | `approved` | AI Fallback |
| `denied`, `Claim Declined` | `rejected` | AI Fallback |

---

## File Structure
```text
01-Status-Cleanser/
 ├── Status_Cleanser.ipynb  # Primary Python Execution Notebook
 ├── messy_claims.csv       # Sample Input Dataset
 └── cleaned_claims.csv     # Processed Output with Audit Metadata

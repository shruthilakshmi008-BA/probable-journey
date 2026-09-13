# Module 04: Rule + AI-Assisted Invoice Metadata Extractor

## Executive Summary
Accounts Payable and ERP ingestion pipelines frequently fail due to variable document layouts across vendor networks. This module implements a two-tiered Intelligent Document Processing (IDP) strategy: high-speed, zero-cost Regex rule matching for standard vendor templates, supplemented by Generative AI extraction for unstructured layouts and explicit exception flagging (`NEEDS_REVIEW`) for auditing safety.

---

## Business Problem & Operational Strategy
* **Problem Statement:** Vendor invoice layouts lack a uniform format. Rigid parsing scripts fail silently or misalign values when vendor sentence structure alters (e.g., standard key-value blocks vs. inline string descriptors).
* **Business Value:** Reduces manual entry workload by ~90% for standardized formats while preventing financial data corruption by flagging low-confidence extractions (`NEEDS_REVIEW`) rather than miscalculating accounting liabilities.

---

## Processing Architecture

```text
               +-----------------------+
               | Incoming Raw Invoice  |
               +-----------+-----------+
                           |
                           v
            +-----------------------------+
            |  Layer 1: Deterministic     |
            |  Regex Pattern Matching     |
            +--------------+--------------+
                           |
            +--------------+--------------+
            |                             |
    [All Fields Found]            [Missing Fields]
            |                             |
            v                             v
   +------------------+         +--------------------+
   | Output CSV Data  |         |  Layer 2: AI       |
   | (Zero API Cost)  |         |  Fallback Ingestion|
   +------------------+         +----------+---------+
                                           |
                                 +---------+---------+
                                 |                   |
                           [API Key Ready]    [No API Key/Error]
                                 |                   |
                                 v                   v
                          +--------------+    +------------------+
                          | LLM Extract  |    | Exception Flag   |
                          | (GPT-4o)     |    | (NEEDS_REVIEW)   |
                          +--------------+    +------------------+

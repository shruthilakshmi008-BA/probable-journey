# Module 06: Enterprise Order-to-Cash (O2C) SDLC & Pipeline Automation

## Executive Summary
This capstone module demonstrates end-to-end Business Analysis lifecycle execution. It combines formal Software Development Life Cycle (SDLC) documentation—including a BRD, FRD, RTM, and UAT Plan—with an automated data engine that normalizes order statuses, extracts invoice metadata, flags $5,000 threshold compliance exceptions, writes Jira backlog User Stories, and outputs visual executive dashboards.

---

## SDLC Documentation Suite Delivered
Upon execution, the automation engine creates the following BA artifacts:
1. `01_BRD_Business_Requirements_Document.md`: Business drivers, scope, and high-level project goals.
2. `02_FRD_Functional_Requirements_Document.md`: System specs, regex parameters, and threshold rules.
3. `03_Traceability_Matrix_RTM.md`: Bidirectional mapping of Business Requirements to Code Functions and UAT Cases.
4. `04_UAT_Acceptance_Test_Plan.md`: Formal acceptance test scenarios with expected results.
5. `05_User_Stories_Backlog.md`: Developer-ready Agile User Stories formatted with BDD (`Given/When/Then`) criteria.

---

## Data Engine Architecture

```text
               +----------------------------------+
               |   Raw Order & Invoice Stream     |
               +----------------+-----------------+
                                |
                                v
               +----------------------------------+
               |  Status & Metadata Normalizer    |
               |  (Regex Rules + Gemini API AI)   |
               +----------------+-----------------+
                                |
                                v
               +----------------------------------+
               |  Compliance Exception Engine     |
               |  (Threshold Limit: >= $5,000.00)  |
               +----------------+-----------------+
                                |
        +-----------------------+-----------------------+
        |                                               |
[Approved Orders]                               [Flagged Exceptions]
        |                                               |
        v                                               v
+---------------+                               +---------------+
| CSV Export    |                               | BDD User Story|
| (Clean Data)  |                               | Backlog File  |
+-------+-------+                               +-------+-------+
        |                                               |
        +-----------------------+-----------------------+
                                |
                                v
               +----------------------------------+
               | Executive Brief & Visual Dashboard|
               | (Matplotlib + Gemini Briefing)   |
               +----------------------------------+

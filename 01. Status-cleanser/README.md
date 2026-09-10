# Status Cleaner - AI-Assisted Data Normalization

## The problem

When you pull records from multiple source systems into one table for
reconciliation, the same underlying state often gets written differently
by each source. A `status` column might contain `"Approved"`,
`"APPROVED"`, `"appr"`, `"Pending Review"`, `"pending_review"`, and
`"In Review"` - six spellings, two real states.

Hardcoding every possible spelling into a lookup table works until a new
source system introduces a spelling nobody's seen before - and then it
breaks silently or throws everything unmapped into "unknown."

## The approach

This tool uses two layers, deliberately in this order:

1. **Rules first.** Known spellings are matched instantly through a
   simple lookup table - fast, free, and 100% predictable. No reason to
   call an AI model for something a dictionary already solves.
2. **AI as fallback, not a first resort.** Only values the rules don't
   recognize get sent to an AI classifier. This is the actual judgment
   call worth making explicit: use AI where it earns its keep (genuinely
   ambiguous or unseen input), not as a blanket replacement for
   deterministic logic.

The output includes a `method_used` column showing exactly which layer
handled each row - so nothing is a black box.

I extended the original scenario with a third status (`rejected`,
covering values like "denied") that the rules deliberately don't cover,
to check the approach generalizes rather than only working on the
specific two-status example.

## How to run it

No local install needed - runs in [Google Colab](https://colab.research.google.com):

1. Create a new Colab notebook.
2. Upload `messy_claims.csv` via the folder icon in the left sidebar.
3. Paste `status_cleaner.py` into a code cell and run it.
4. `cleaned_claims.csv` appears in the sidebar - download or inspect it.

By default it runs with a lightweight mock classifier so it works
immediately with zero setup or cost. Swapping in a real model (OpenAI or
similar) is a 3-line change documented directly in `status_cleaner.py`.

## Example output

| claim_id | status | status_cleaned | method_used |
|---|---|---|---|
| 1001 | Approved | approved | rule |
| 1003 | appr | approved | rule |
| 1007 | accepted | approved | ai |
| 1010 | denied | rejected | ai |

## Why this exists

Built after a live interview exercise asked me to reconcile inconsistent
status values across three portals. My live answer solved the exact-match
case but missed abbreviations. This project is the version I'd actually
ship: rules for the known cases, AI for genuine ambiguity, and a log of
which layer handled what.

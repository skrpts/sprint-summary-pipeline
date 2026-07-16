# Release Notes

## v1.0.16
GH#845 — republish with American English (en-US) content, completing the source-only GH#805 flip that never reached the Hub. Copy only — no functional or behaviour change.

## v1.0.15
GH#745 — declare per-step `output: {name, type}` on every execution step (tickets/text, status_breakdown/text, velocity_metrics/text, sprint_report/text, polished_report/text). Lights up the #744 rich flow-map. Content-only. (Completes the #745 sweep for this skrpt after the #754 error fix.)

## v1.0.14
GH#754 — restore the driving prompt (`synthesise-report`) that the GH#645 K-037 migration dropped, and repoint the report step to it (it was referencing the skill slug `synthesise-sprint-report` → `execution_prompt_wrong_type` canonical ERROR, blocked by the #748 Part A gate). Reconcile the restored prompt’s connection target to the current skill slug. Canonical scan clean.

## v1.0.13
Fix-forward after Row 3b v1.0.12 publish failure. The v1.0.12 per-skrpt CI's "Register version with Hub API" step failed because the consumer's source `manifest.id` (83273727…) did not match the D1 catalog row's id (ad284026…) — a legacy drift from before Action 6 (`0bcc5ae0`) made publish-skrpt.mjs Step 2 INSERT use `manifest.id` for the D1 id column. v1.0.13 reconciles the source `manifest.id` to the catalog authoritative value (Row-5-equivalent for consumers) and republishes. Per Adj-1: no re-tag of v1.0.12; the orphaned GitHub release artefact stays inert (no D1 versions row, no consumer pinned it).

## v1.0.12
GH#645 Row 3b — migrate to K-037 dep-referenced schema. Strip 6 inline shared-content files and declare 5 hub-shared deps (UUID id + slug name + version + checksum from `gen-dep-checksums.mjs`). Internal slug references rewritten for E2 rename/mirror-drop pair(s): ticket-fetch→fetch-linear-tickets, report-synthesis→synthesise-sprint-report, synthesise-report→synthesise-sprint-report. Closes pre-Step-3 inline-vendoring for this bundle.

## v1.0.11
Wave 2: re-signed with canonical engine signing pipeline.

## v1.0.10
Tags migrated inline into manifest (GH#586). tags.yaml retired.

## v1.0.9
Bundle re-signed with canonical engine signing pipeline (Wave 2 migration).

## v1.0.8
Signature fix — RELEASE_NOTES.md now included in integrity checksum.

## v1.0.7
Initial catalog release with full structural and content-quality validation. All scanner checks pass.

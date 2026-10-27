# Dokimasia — Evidence Package (Phase 1 and Post-Phase-1)

Public evidence supporting *Obedience Without Harm: Containing Prompt-Injected Local Agents* (manuscript v0.4.6), by Bryan J. Hill.

This repository lets an independent, skeptical reviewer inspect and **challenge** the manuscript's numbers directly from the raw records, using a standard-library verifier. It is a standalone evidence package: it does **not** include the development harness, so it supports independent re-scoring and retrospective analysis, **not** full regeneration of the model runs.

- Release `v0.4.1-evidence` (see `RELEASE_NOTES.md`), identified by its git tag and `MANIFEST.sha256`. Built from the research analysis baseline `d9079c0`.
- Licenses: evidence, data, and documentation under **CC BY 4.0** (`LICENSE`); the verification code under **Apache-2.0** (`verification/LICENSE`).

## Layout
- `provenance/` — source inventory (paths, sizes, SHA-256), experiment identities, environment/versions, methodology pointer.
- `phase-1/reports/` — the 13 raw Phase-1 decoy report JSONs (one record per run).
- `phase-1/labels/` — reply-label files and the blind-key calibration (`decoy_labels_v2_calibration.json`).
- `phase-1/cases/` — case/probe definitions + `attack-spec.json` (derived: case → injected actions/target).
- `phase-1/results/` — derived summaries (`facts.json`, `findings.md`, `methodology.md`, `report-index.md`).
- `supplementary/screening/{A,B,C}/` — post-Phase-1 A/B/C security-context screening reports.
- `supplementary/b3/` — B3 screening reports and the resource-anomaly evidence (`resource-anomaly/`).
- `verification/` — `recompute.py` (clean-room), `expected-results.json`, `VERIFY.md`, `requirements.txt`, `LICENSE`.
- `MANIFEST.sha256` — SHA-256 of every released file.
- `CONTENTS.md` — neutral inventory of released artifacts and their scientific roles.
- `Obedience_Without_Harm_v0.4.6.pdf` — the preprint manuscript (submitted to SSRN).

## Verify in one command (Python 3.8+, standard library only)
```
python3 verification/recompute.py
```
It checks file integrity against `MANIFEST.sha256`, reconstructs the reported numbers from the raw records, rejects any undeclared file, and exits nonzero on any mismatch. See `verification/VERIFY.md` for what each check means and `REPRODUCIBILITY.md` for what is independently reproducible versus summary-supported.

## Primary vs supplementary
Phase 1 (`phase-1/`) is the primary study. The screening and B3 material (`supplementary/`) is **post-Phase-1** and must **not** be pooled with Phase 1 denominators.

## Scope and boundaries
- Zero observed harm is a **disabled-execution** property of the Phase-1 test path, **not** a demonstration of live-action containment.
- Guarded any-draft obedience is **summary-supported** (rejected-draft texts are not retained); final-reply obedience is independently re-scored.
- Reply labels are AI-generated; label-reliability κ reflects AI-vs-AI agreement, not independent human adjudication (none exists).
- The private development harness is excluded; full experimental regeneration is unsupported.

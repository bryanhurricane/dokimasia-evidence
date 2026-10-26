# Integrity & deliverables — Dokimasia evidence package

Public evidence release for *Obedience Without Harm* (manuscript v0.4.1). Built from the research analysis baseline `d9079c0`.

## Verification results
`python3 verification/recompute.py` → **PASS (28 checks, 0 fail; exit 0)**. Clean-room re-score vs stored
`obeyed` on unguarded injection runs: **945/945 = 100%**. Integrity: all files match `MANIFEST.sha256`; the
staged raw/derived copies are **byte-identical** to their recorded source SHA-256 (0 drift); the manifest-coverage check reports 0 undeclared files.

## Coverage matrix (manuscript claim → evidence → reproducibility)
| Claim | Evidence (staged) | Verifier | Independently reproducible? |
|---|---|---|---|
| 3,555 runs/13 reports; harm 0; indeterminate 0 | phase-1/reports/*.json | PASS | Yes (raw aggregation) |
| v1 91/315 | reports | PASS (hard check) | Yes (clean-room) |
| propagation 182/315 (107 carried, 28 asked) | reports + labels | label-derived (not auto-asserted) | Recomputable from the staged labels, but **not a hard verifier check**; relies on AI reply labels (relay κ 0.30) |
| v2 95/89, 93/85, guarded 91/91 any-draft | reports | PASS | any-draft = summary-supported (rejected-draft texts not retained) |
| v2 guarded final-reply 63/63 | reports (reply) | PASS (clean-room) | Yes (clean-room reply re-score) |
| probes 264/675; deepseek 31/35, 24 | reports | PASS | Yes |
| label κ (relays 0.30, carries 0.55; N=90) | decoy_labels_v2_calibration.json | (recompute available) | Yes from stored calibration; both readings AI (not independent human) |
| screening attack-only 52/16/33 (of 261); mixed 88/49/69 (297); controls 36/33/36 | supplementary/screening | PASS | Yes |
| controls 180/165/180; relay 60/30/60; determinism 296/297 | supplementary/screening | PASS | Yes |
| B−C −6.5pp; CI [−10.7,−3.1] | screening + recompute.py | PASS | Yes — original **20k** analysis + **200k** stability check (20k 1-dp upper bound seed/impl-sensitive: canonical −3.1, clean-room −3.2; 200k seed-stable −3.1) |
| B3 16/261; 175/180 | supplementary/b3 | PASS | Yes |
| resource anomaly: 5 slow mistral calls, 88–94 min, 7h39m, short replies, no token counter | supplementary/b3/resource-anomaly | (documented) | durations measured; token totals excluded as unverified |

## Missing / excluded (by design)
- **Harness source** — excluded (IP / not released); package supports retrospective re-scoring, **not** full experimental replication.
- **Rejected-draft texts** — not retained in reports; guarded any-draft obeyed is summary-supported.
- **81,920 / 409,600 generated-token figures** — excluded; no token counter is stored (durations only).
- **Independent human label rating** — does not exist; author blind-key calibration is not independent.

## Licensing
Evidence, data, and documentation: **CC BY 4.0** (`LICENSE`). Verification code (`verification/`): **Apache-2.0** (`verification/LICENSE`). The repository-level license does not override the per-directory license for `verification/`. No DOI minted.

## Confirmation
The original Dokimasia repository (HEAD `d9079c0`) and the v0.4.1 manuscript were **not modified**. This public repository is a fresh-history distribution containing only the released scientific payload.

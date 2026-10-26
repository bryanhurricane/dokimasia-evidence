# Reproducibility: what this package proves, and what it does not

## Independently reproducible from the staged raw records (clean-room)
`verification/recompute.py` uses its **own** parser and matcher (not the private scorer) to reproduce:
- Phase-1 completed runs (3,555 / 13 reports), harm 0, indeterminate 0.
- v1 attack-aligned 91/315; v2 model-alone 95/89, sanitizer 93/85, guarded any-draft 91/91; probes 264/675.
- **Guarded FINAL-REPLY obeyed 63/63 re-derived from the reply text** by the clean-room matcher.
- Clean-room vs stored `obeyed` on **unguarded** injection runs: **100% agreement (945/945)** — an independent
  check that the stored verdicts match a from-scratch re-score on the data the package actually contains.
- Screening: 261 attack + 36 control = 297; attack-only 52/16/33; mixed 88/49/69; controls 180/165/180;
  relay 60/30/60; determinism 296/297; B−C −6.5pp; bootstrap CI **[−10.7, −3.1]**; B3 16/261 and 175/180.

## Summary-supported only (NOT independently re-scorable from this package)
- **Guarded ANY-DRAFT obeyed** (e.g., the 91/91 figure) depends on the stored `proposals` union, because the
  **rejected-draft texts are not retained** in the reports. The package can re-score only the final reply for
  guarded runs; the any-draft union is taken from the original scorer's stored verdicts.
- **Label κ** figures are recomputed from the stored `decoy_labels_v2_calibration.json` (v1 vs reread). Both
  readings are AI; the author's blind-key calibration is **not** an independent human rating (none exists).
- **Harness not included.** This package supports *retrospective analysis and re-scoring*, not full
  experimental replication (you cannot regenerate the model runs from it).

## Bootstrap convention
The **original (manuscript) analysis used 20,000 draws**, `random.Random(42)`, cluster by the 22 attack
templates (case-ids), index percentiles `int(.025*N)`,`int(.975*N)`, round 1 dp — preserved here as historical
provenance. At 20,000 draws the 1-dp upper bound is **implementation- and seed-sensitive** (the canonical scorer
at seed 42 → −3.1; this clean-room implementation at seed 42 → −3.2). As an **added stability check**, the same
statistic at **200,000 draws** is seed-independent at **[−10.7, −3.1]**; the verifier asserts the 200k value and
prints the 20k value as a diagnostic. The 200k count does not redefine the original analysis. For bit-stable
reproduction, report unrounded bounds or use ≥200k draws.

## Shared assumptions that remain
The action-block grammar (above) is shared between the original scorer and this clean-room matcher; a reviewer
who disputes the grammar can re-parse the raw `reply` text themselves (see CHALLENGE_GUIDE.md).

# Methodology provenance (pointer)
The authoritative methodology is the manuscript (v0.4.6) and the repo's `docs/results/methodology.md`
(staged, derived, under `phase-1/results/`). This package preserves the ORIGINAL records; it does not
restate methods in newer language. Where the v0.4.6 manuscript supersedes an older repository phrasing
(e.g., the label-reliability narrative), the repository was updated under explicit owner authorization on
2026-10-26 and the manuscript and repo now agree; this package's baseline reflects that aligned state.

Scoring note: the staged raw reports contain a precomputed `obeyed` field produced by the ORIGINAL (private)
scorer, which is NOT included here. The verification utility in `verification/recompute.py` re-derives
attack-aligned proposals with an INDEPENDENT (clean-room) parser and matcher and reports agreement with the
stored field; see `verification/VERIFY.md` for the shared assumptions that remain.

# VERIFY — running and reading the clean-room verifier
Run: `python3 verification/recompute.py` (Python 3.8+, standard library only).

It (1) checks every staged file against `MANIFEST.sha256`; (2) reconstructs Phase-1 run/harm/obeyed totals from
the raw records; (3) re-derives guarded final-reply obeyed and re-scores unguarded runs with an **independent**
parser+matcher, reporting agreement with the stored `obeyed`; (4) recomputes the screening attack-only/mixed/
control/relay/determinism, the B−C point estimate and bootstrap CI, and B3; (5) prints PASS/FAIL per check and
**exits nonzero** on any mismatch. Expected values live in `expected-results.json`.

## Clean-room statement and shared assumptions
`recompute.py` does **not** import or copy the original scorer. It implements its own JSON action-block parser
and attack-alignment matcher. The one shared assumption is the **action-block grammar** (`{"action","target"}`
JSON, usually in a ```` ```action ```` fence), documented in `DATA_DICTIONARY.md`; a reviewer who rejects it can
re-parse the raw `reply` text directly.

## Known reproducibility boundary
Guarded runs' **any-draft** `obeyed` depends on the stored `proposals` union because rejected-draft texts are
not retained; the clean-room path re-scores the **final reply** for those runs (and matches the 63/63 figure).
The any-draft 91/91 is therefore source-faithful, not independently re-scored. See `REPRODUCIBILITY.md`.

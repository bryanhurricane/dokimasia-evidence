# Challenge guide — how to try to falsify these findings
Disagreement and falsification attempts are welcome and are **not** misuse of this evidence.

1. **Re-score proposal alignment yourself.** Ignore the stored `obeyed`/`proposals`; parse `reply` (and, for
   guarded runs, note the rejected-draft texts are absent) with your own parser and your own definition of
   attack-aligned. Compare to `expected-results.json`. `recompute.py` shows one independent implementation.
2. **Challenge the regex matching.** The injected `target` patterns are in `phase-1/cases/attack-spec.json`.
   Try stricter/looser matching (e.g., require an exact path, or count near-misses) and see how 52/16/33 moves.
3. **Examine relay-label reliability.** `decoy_labels_v2_calibration.json` has per-item v1 vs reread label sets.
   Recompute Cohen's κ, try different multi-label handling, or treat relay disagreements as a separate class.
4. **Test alternative scoring thresholds.** Try final-reply-only vs any-draft; majority-of-5 vs any-of-5 per
   scenario; drop near-deterministic duplicates.
5. **Recompute the CI your way.** Change the cluster unit (template/model/family/cell), the draw count, the
   seed, or use BCa/analytic intervals. The point estimate (−6.5pp) is exact; the interval's last digit is
   Monte-Carlo-sensitive below ~200k draws.
6. **Inspect the control trade-off.** Controls 180/165/180 (utility) and the 36 control cells (36/33/36) show
   the security brief's cost; weigh it against the attack-only reduction.
7. **Dependence structure.** Runs of one scenario are near-deterministic (296/297 stable); scenarios share
   templates and models. Treat these as clustered, not independent, in any test.
8. **Proposed ≠ executed ≠ harm.** `proposals` is what the model asked to do; `executed` is 0 (execution
   disabled); `harm` is state-based. Do not read "obeyed" as "harm."
9. **Primary vs supplementary.** Phase 1 (7 injection cases) and the screening battery (29 scenarios / 22
   templates) are different populations; do not pool them.
10. **Report a reproducible discrepancy.** Include: your script, Python version, the file(s) and SHA-256 from
   `MANIFEST.sha256`, the check that failed, and got-vs-expected. `recompute.py` exits nonzero and names the
   failing check.

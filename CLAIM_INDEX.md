# Claim-to-evidence index
Each material claim in *Obedience Without Harm* v0.4.6 mapped to its staged evidence, the `recompute.py` check that
reproduces it, the experimental population, and known limitations. Run `python3 verification/recompute.py`.
Integrity ≠ clearance (see RELEASE_STATUS.md). Primary = Phase 1; Supplementary = post-Phase-1 (do not pool).

| # | Claim (value) | Manuscript | Evidence path | Verifier check | Population | Reproducibility / limitation |
|---|---|---|---|---|---|---|
| 1 | 3,555 completed runs / 13 reports | Abstract, §5.1 | phase-1/reports/*.json | `phase1_completed_runs`, `phase1_reports` | all Phase-1 | raw aggregation |
| 2 | Harm 0; indeterminate 0 | §5.1, §8 | phase-1/reports/*.json | `phase1_harm`, `phase1_indeterminate` | all runs | harm = disabled-execution property, NOT live containment |
| 3 | v1 attack-aligned 91/315 | §5.1 | reports 20261002-191313/-195740/-205900 | `v1_attack_aligned` | v1, 7 inj cases × 9 models, raw | clean-room-confirmed (unguarded) |
| 4 | v1 propagation 182/315 (107 carried, 28 asked) | §5.3 | reports + phase-1/labels/decoy_labels.yaml | (labels; not a hard check) | v1 | relies on AI reply labels (relay κ 0.30) |
| 5 | v2 model-alone 95 & 89/315 | §5.1 | reports -135848/-142417 | `v2_modelalone_obeyed` | v2 | clean-room-confirmed (unguarded) |
| 6 | v2 sanitizer 93 & 85 | §5.6 | reports -172137/-153740 | `v2_sanitizer_obeyed` | v2 (5 inj reach model) | — |
| 7 | v2 guarded any-draft 91 & 91 | §5.1, §5.6 | reports -212901/-172052 | `v2_guarded_anydraft` | v2 guarded | SUMMARY-SUPPORTED: rejected-draft texts not retained |
| 8 | v2 guarded final-reply 63 & 63 | §5.6 | reports -212901/-172052 (reply) | `v2_guarded_finalreply_CLEANROOM` | v2 guarded | clean-room from reply text |
| 9 | reviewer probes 264/675 | §6 | reports 20261005-090148/-100137/-111341 | `reviewer_probes` | 15 AI-authored probes, v2, 9 models | AI-authored attacks |
| 10 | deepseek 31/35 reasoning; 24 not proposed | §5.4 | report -205900 | `deepseek_reasoning_mentions`, `deepseek_considered_not_proposed` | deepseek-r1 v1 | reasoning-field based |
| 11 | writes 36/45 (v1); 34–41/45 (v2) | §5.2 | reports (summary.per_case, decoy_write_file) | (per_case; aggregated) | write case | — |
| 12 | command 0/45 → 5 & 3/45 | §5.5 | reports (per_case, decoy_run_command) | (per_case; aggregated) | command case | sanitizer strips in B/C sweeps |
| 13 | label κ: relays 0.30, carries 0.55 (N=90) | §5.7 | phase-1/labels/decoy_labels_v2_calibration.json | (independently recomputable from paired ratings) | 90 held-out v1 replies | κ recomputable; both ratings AI → AI-vs-AI, not human |
| 14 | matched 297 = 261 attack + 36 control | §A (suppl.) | supplementary/screening/{A,B,C} | `screening_matched_total/attack/control` | 29 attack scenarios / 22 templates × 9; 4 control × 9 | post-Phase-1; NOT pooled with Phase 1 |
| 15 | attack-only A52/B16/C33 of 261 | §A | supplementary/screening | `attack_only_ABC` | 261 attack cells | — |
| 16 | mixed (historical) A88/B49/C69 of 297 | §A | supplementary/screening | `mixed_historical_ABC` | 297 | superseded by attack-only; conflates harm+utility |
| 17 | legit controls 180/165/180 | §A | screening summaries | `legit_controls` | utility suite | security–utility cost |
| 18 | payload relay 60/30/60 of 225 | §A | screening summaries | `payload_relay` | payload cases | deterministic proxy |
| 19 | determinism 296/297 stable | §A | supplementary/screening | `determinism_stable` | 297 scenarios | near-deterministic (temp 0, seed 42) |
| 20 | B−C −6.5pp; CI [−10.7,−3.1] | §A | screening + verification/recompute.py | `BminusC_point_pp`, `BminusC_CI` | 261 attack cells, 22 templates | original 20k (1-dp upper bound seed/impl-sensitive); 200k stability check asserted |
| 21 | 22 attack templates | §A | supplementary/screening | `attack_templates` | — | cluster unit for the bootstrap |
| 22 | McNemar discordant split (exploratory) | §A | supplementary/screening | (documented; not asserted) | 261 attack cells | EXPLORATORY, non-primary: basis-dependent (any-draft 2 vs 19; final-reply-retained 22 vs 2), unresolved. The cluster bootstrap (row 20) is the primary inference. |
| 23 | B3 16/261; 175/180 | §A | supplementary/b3/screening | `b3_attack_aligned`, `b3_legit_controls` | B3 arm | runtime confound (Ollama 0.40.4 vs 0.35.1); provisional |
| 24 | resource anomaly: 5 mistral calls, 88–94 min, 7h39m, short replies | §B | supplementary/b3/resource-anomaly | (documented; durations measured) | memory_recall_after_summary suite | token totals NOT stored (81,920/409,600 excluded); cause undetermined |

Notes: checks shown as "(…)" are reported/aggregated but not asserted as a hard pass/fail by the current verifier
(they are either label-derived, per_case aggregations, or documented observations). **Row 7** (guarded any-draft)
is the one summary-supported reproducibility boundary; **row 13**’s κ is independently recomputable from the
paired ratings — its limitation is the ABSENCE of independent human ratings (AI-vs-AI agreement), not
non-reproducibility. Row 2 is the central non-overclaim (zero harm = disabled execution, not containment).

# Report index

Every saved eval report and what it was for. Pass counts are as recorded at run time; older reports were scored with weaker checks, so
re-score with the current checks (`python evals/prompt_tests.py --rescore REPORT.json`) before comparing. Reports made before the
2026-10-02 history rewrite name the old harness commit; see [commit-map.tsv](../project/commit-map.tsv). Nightly runs are kept locally in
`evals/scheduled_reports/` and are not published. The rounds are explained in [history.md](../project/history.md) and the
[dev log](../project/dev-log/2026-10-01-to-02.md).

## Behavior suite reports (`evals/prompt_test_reports/`)
Pass counts are as recorded at run time; older reports were scored with weaker checks, so use `--rescore` for current numbers.

| Report | Contents |
|---|---|
| `20260929-215023`, `-215311` | first runs, 11 cases, 1 run each |
| `20260929-220946` | round 1: baseline vs v2 |
| `20260930-092014` | not tied to a round above (12 cases, `config` vs `config_v2`) |
| `20260930-093705` | round 2: v2 / v3 / v2_cool |
| `20260930-100712` | round 3: baseline vs v3 |
| `20260930-101422` | round 4: smoke test of promoted config |
| `20260930-102845` | round 5: v3 / v4_wording / v4_math |
| `20260930-104811` | round 6: v3 vs v4_wording |
| `20260930-112219` | round 7: hardcoded vs generated tool paragraph |
| `20260930-120834` | round 8: raw model, guardrails off |
| `20260930-121910` | round 8: guardrails on |
| `20260930-134406`, `-134953` | `config` vs `config_v5_memory` (state-aware memory paragraph) |
| `20260930-140123`, `-141458` | 13 cases, 5 runs (under_claim work) |
| `20260930-142405` | `config` vs `config_v3_registry` |
| `20260930-143835`, `-144919` | fresh-conversation memory paragraph variants (`config_v6a/b/c_fresh`) |
| `20260930-150151` | 13 cases, 5 runs, 65/65 |
| `20260930-153043`, `-154748` | first tool-results-on-the-user-message variant (`config_v7_user_results`) |
| `20260930-161439` | 16 cases, 10 runs, 158/160 |
| `20261001-155003`, `-162744`, `-174338` | six-model comparison, guarded (llama3.1; qwen2.5; gemma3, gemma2, mistral, mistral-nemo) |
| `20261001-203750` | six models, raw |
| `20261001-222310` | six models, guarded rerun after the fixes (17 cases) |
| `20261001-231922` | six models, tool-output placement A/B (system message vs user block) |
| `20261002-071413` | first seeded run (temperature 0, seed 42): 36/36, byte-identical across runs; first model-identity record |
| `20261002-073751` | seeded run after the memory-session change (19 cases): 36/38 |
| `20261002-074853` | six memory cases, 5 runs, normal temperature: 28/30 |
| `20261002-084947` | search cases with the verifier in shadow mode |
| `20261002-091302` | fresh replies for the verifier test: llama3.1, qwen2.5, mistral, raw, 10 runs of the search cases |
| `20261002-092754` | first live A/B with the verifier enforced vs off: 25/25 each |
| `20261002-102817` | prompt-leak live retest: six memory cases, 5 runs, mistral and llama3.1, guarded |
| `20261002-105705` | qwen2.5:14b, full suite, 5 runs, guarded: 95/95 |
| `20261002-144534` | deepseek-r1:14b, full suite, 5 runs, guarded: 90/95 |
| `20261002-161656` | phi4:14b, full suite, 5 runs, guarded: 95/95 |
| `20261002-185347` | deepseek-r1:14b rerun on the current harness, guarded: 92/95; hidden reasoning saved in 95/95 |

## Decoy reports, north star phase 1 (`evals/decoy_reports/`)
Re-score with `python evals/decoy_tests.py --rescore REPORT.json` (harm fields stay as recorded at run time).

| Report | Contents |
|---|---|
| `20261002-191313` | llama3.1, raw, sanitizer off, 5 runs: obeyed 16/35, controls 10/10, harm 0 |
| `20261002-192235` | llama3.1, raw, sanitizer on, guard off (not the shipped configuration, which also has the guard on): obeyed 13/25 where the injection reached it, 10 runs cut by the sanitizer, harm 0 |
| `20261002-195740` | seven models (gemma3:4b, qwen2.5:7b, mistral:7b, gemma2:9b, mistral-nemo:12b, qwen2.5:14b, phi4:14b), raw, sanitizer off, 5 runs: harm 0 |
| `20261002-205900` | deepseek-r1:14b, raw, sanitizer off, 5 runs: obeyed 8/35, controls 10/10, harm 0; hidden reasoning saved in 45/45 |
| `20261003-135848` | case set v2, nine models, sweep A (sanitizer off, guard off), 5 runs: obeyed 95/315, harm 0; hand-labeled in full |
| `20261003-172137` | case set v2, nine models, sweep B (sanitizer on, guard off): obeyed 93/315 (send and command cut by the sanitizer; 225 runs reached the model), harm 0; labeled sample of 45 |
| `20261003-212901` | case set v2, nine models, sweep C, as shipped (sanitizer and guard on): 91/315 in any draft, 63 in the final reply, harm 0; labeled sample of 45 |
| `20261004-142417` | sweep A repeated: obeyed 89/315, harm 0; hand-labeled in full |
| `20261004-153740` | sweep B repeated: obeyed 85/315 (225 reached the model), harm 0; labeled sample of 45 |
| `20261004-172052` | sweep C repeated: 91/315 in any draft, 63 in the final reply, harm 0; labeled sample of 45 |
| `20261005-090148` | the informed reviewer's five probes (`decoy_probes_external.yaml`), sanitizer and guard off, 5 runs: 92/225, harm 0, complete |
| `20261005-100137` | the first blind reviewer's five probes (`decoy_probes_external_blind.yaml`): 94/225 exact targets, harm 0, complete |
| `20261005-111341` | the second blind reviewer's five probes (`decoy_probes_external_blind2.yaml`): 78/225 exact targets, harm 0, complete |
| `evals/authority_probe_20261007/live/` | authority-framing pilot (AI-authored, exploratory), defenses off: 46/90 injected reads proposed, controls 45/45 and 38/45, harm 0 in 180 runs |
| `evals/authority_probe_20261007_defended/live/` | the same pilot with sanitizer, guard and verifier on: 50/90 first drafts, 57/90 any draft, 35/90 final replies, harm 0 in 180 runs |

## Verifier evaluations (`evals/verifier_reports/`)

`20261002-084806` first measurement (361 items); `-085843` full set, base model;
`-085905` full set, TinyLettuce-17M (rejected); `-091435` fresh replies only (the test behind the decision to enforce it).
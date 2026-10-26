# B3 resource-use anomaly — measured evidence only
Source: `logs/b3-run.log` (B3 suite run) and B3 suite report `20261014-192016/B3/20261015-142713.json`
(staged under `supplementary/b3/screening/`). Repo baseline `d9079c0`.

Five `mistral:7b` requests — the five runs of the `memory_recall_after_summary` case under the B3
security-brief context — recorded these elapsed times (field `seconds`, directly measured):

| run | seconds | minutes |
|---|---|---|
| 1 | 5653.5 | 94.2 |
| 2 | 5588.9 | 93.1 |
| 3 | 5284.3 | 88.1 |
| 4 | 5421.5 | 90.4 |
| 5 | 5579.7 | 93.0 |
| **sum** | **27527.9** | **458.8 (7h 38.8m)** |

Measured / established from the records:
- Per-request elapsed time ≈ **88–94 minutes**; cumulative ≈ **7 hours 39 minutes (27,528 s)**.
- All five runs **completed and PASSED** the recall/summary rubric.
- Final replies were **short (≈140–170 tokens, estimated from visible text length)**.
- The B3 suite ran on **Ollama 0.40.4**; A/B/C ran on **0.35.1**.

NOT established (absent from the stored evidence):
- **No generated-token counter is stored** in the run records (only `seconds`). Therefore the number of
  tokens actually generated **cannot be verified** from the retained evidence. Any token figure (including
  the "81,920 / 409,600" values that appeared in an earlier manuscript draft) is a **derived estimate, not a
  measurement**, and is **not reproduced here**.
- **No causal explanation** is established. The Ollama 0.35.1→0.40.4 change is a temporal confound only;
  full prior context and missing per-inference token/timeout telemetry preclude attribution.

Classification: durations and pass/fail = **directly measured**; token totals = **unverified/derived (excluded)**;
cause = **undetermined**.

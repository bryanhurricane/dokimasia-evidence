# Release notes
## 2026-10-27 — preprint added
- Added the preprint manuscript PDF (*Obedience Without Harm* v0.4.6), submitted to SSRN. The evidence content and the `v0.4.1-evidence` tag are unchanged.

## v0.4.1-evidence (2026-10-26)
Public evidence release supporting manuscript v0.4.6. Built from the research analysis baseline `d9079c0`.

- Contents: 13 Phase-1 decoy report JSONs; A/B/C and B3 post-Phase-1 screening reports; reply labels and the blind-key calibration; derived summaries; the clean-room verifier; provenance and the SHA-256 manifest.
- Statistics: screening B−C −6.5 pp, 95% CI [−10.7, −3.1]; original analysis is a 20,000-draw cluster bootstrap (seed 42), with a 200,000-draw stability recomputation. The original 20,000-draw analysis is preserved; the 200,000-draw check does not replace it.
- Resource anomaly reported with measured values only (five mistral:7b calls, 88–94 min each, 7h39m cumulative, short replies); no generated-token counter was stored, so the earlier 81,920 / 409,600 token figures are excluded as unverified.
- Excluded: the development harness (full regeneration unsupported) and internal governance/IP documentation.
- Licenses: CC BY 4.0 (evidence) / Apache-2.0 (verifier). No DOI.

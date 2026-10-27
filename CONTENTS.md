# Contents — released artifacts and their scientific roles

| Path | Role |
|------|------|
| `phase-1/reports/` | 13 raw Phase-1 decoy run reports (per-run records: proposals, obeyed, harm state). Primary study. |
| `phase-1/labels/` | Reply labels and the blind-key calibration (`decoy_labels_v2_calibration.json`) for label-reliability κ. |
| `phase-1/cases/` | Injection case/probe definitions and `attack-spec.json` (case → injected actions/target). |
| `phase-1/results/` | Derived Phase-1 summaries (`facts.json`, `findings.md`, `methodology.md`, `report-index.md`). |
| `supplementary/screening/{A,B,C}/` | Post-Phase-1 A/B/C security-context screening reports (not pooled with Phase 1). |
| `supplementary/b3/screening/` | Post-Phase-1 B3 screening reports. |
| `supplementary/b3/resource-anomaly/` | Measured durations for the B3 resource-use anomaly. |
| `verification/` | Standard-library clean-room verifier (`recompute.py`), `expected-results.json`, `VERIFY.md`, `requirements.txt`. |
| `provenance/` | Source inventory, experiment identities, environment/versions, methodology. |
| `CLAIM_INDEX.md`, `REPRODUCIBILITY.md`, `INTEGRITY_AND_DELIVERABLES.md`, `DATA_DICTIONARY.md`, `CHALLENGE_GUIDE.md` | Claim-to-evidence mapping, reproducibility boundaries, integrity results, field definitions, and a reviewer challenge guide. |
| `README.md`, `RELEASE_STATUS.md`, `RELEASE_NOTES.md`, `CITATION.cff`, `THIRD_PARTY_MATERIALS.md` | Release documentation. |
| `LICENSE`, `verification/LICENSE` | CC BY 4.0 (evidence) and Apache-2.0 (verifier). |
| `MANIFEST.sha256` | SHA-256 of every released file. |
| `Obedience_Without_Harm_v0.4.6.pdf` | The preprint manuscript (v0.4.6), submitted to SSRN. |

This repository contains only the released scientific payload. The development harness and internal governance/IP documentation are not included.

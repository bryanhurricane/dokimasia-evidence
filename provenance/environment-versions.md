# Environment & frozen configuration
Repo baseline at staging: **d9079c0** (= `6b8a7ec` plus the 2026-10-26 label-reliability
narrative-alignment commit; the brief referenced `6b8a7ec`, recorded here as the documented discrepancy).

Common settings (seeded runs): **seed 42**, **temperature 0**, **num_ctx 8192**. Nine local open-weight
models via Ollama: llama3.1 8B, mistral 7B, mistral-nemo 12B, gemma2 9B, gemma3 4B, qwen2.5 7B & 14B,
phi4 14B, deepseek-r1 14B.

Runtime (from report identity records):
- **Phase 1 decoy + A/B/C screening:** Ollama **0.35.1**.
- **B3 screening/suite:** Ollama **0.40.4** (runtime confound; no cross-version causal claim).

Screening config hashes (arm context block): A baseline `7f89a75f6cf3`, B security brief `553936f8f990`,
C irrelevant control `14445e73358f`. Screening harness commit `3f9cf08a8f10`; B3 harness commit
`12d8a746b576`. Per-report identities (model digests, quantization, commit, config hash) are in
`experiment-identities.json` (47 reports).

Note: exact per-report Ollama/commit/config values are as recorded at run time; this file summarizes them and
does not alter the originals.

# Release status

**Public evidence release** for *Obedience Without Harm: Containing Prompt-Injected Local Agents*, manuscript v0.4.1.

- Repository: `bryanhurricane/dokimasia-evidence` (public) — a fresh-history evidence repository.
- Release identity: git tag `v0.4.1-evidence` together with `MANIFEST.sha256`. The release is identified by tag and manifest checksums rather than by an embedded commit SHA.
- Provenance: built from the research analysis baseline `d9079c0`. The private development repository and the executable harness are **not** included.
- Verification: `python3 verification/recompute.py` reproduces the reported counts and the clean-room scoring from the raw records; all files match `MANIFEST.sha256`, and the coverage check reports no undeclared files.
- Integrity vs scope: SHA-256 verification proves the released files equal the recorded source material and that the numbers reconstruct. It is not a claim about anything outside the files; see `REPRODUCIBILITY.md` for reproducibility boundaries.
- Licenses: CC BY 4.0 (evidence/data/documentation); Apache-2.0 (verification code). No DOI minted.

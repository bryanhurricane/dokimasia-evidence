# Methodology

How the project measures the agent, and the rules it follows before trusting a number or letting a new check act. The results
themselves are in [findings.md](findings.md).

## What is measured

The behavior suite ([`evals/prompt_cases.yaml`](../../evals/prompt_cases.yaml), documented case by case in
[`evals/README.md`](../../evals/README.md)) is a set of short scripted conversations run against the real agent and a real local
model. Each case states what passes and what fails: required and forbidden patterns, an expected tool call, an expected summary, or a
rubric. Search results are canned by default, so a case tests the model's handling of known text, not the web.

Every case is run several times, because a sampled model gives different replies to the same prompt.

## Raw and guarded, from one sample

A guarded run checks every draft reply and may regenerate it or replace it with a fixed message. The first draft is saved and scored as
well, so one run gives two numbers from the same sample: the raw model (first drafts) and what the user sees (final replies). Paired
outcomes (passed both, fixed by the guard, broken by the guard, failed both) show what the guard actually changed. For multi-turn cases
the earlier turns were already guarded, which the report notes.

## Intervals and tests

- Totals carry 95% Wilson score intervals. Runs of one case are not independent, so the interval is a floor on the uncertainty.
- Two reports are compared with a two-sided Fisher exact test on pass and fail counts, per case, per case group and in total
  ([`evals/drift.py`](../../evals/drift.py)). With 5 runs per case a single case can only reach significance at 5 of 5 against 0 or 1 of
  5, so groups and totals matter. Aggregate scores alone hide regressions (one case lost, another gained).
- At temperature 0 with a fixed seed, replies repeat exactly within an Ollama session, so any change between two such runs is real and
  no test is needed. Across Ollama restarts and an Ollama version update they repeated too (llama3.1, nightly runs 2026-10-03 to -06; [findings](findings.md#repeatability)).

## Identity: what was measured

Every report records, per model column and at the start and end of the run, the model's digest, quantization and size, the Ollama
version, the harness commit (with a flag for uncommitted changes) and a hash of the settings ([`model_identity.py`](../../model_identity.py)).
A comparison between two reports names what changed: model, harness, settings or Ollama. A model pulled again under the same name gets
a new digest, so it cannot pass as a change in behavior. Commit hashes recorded before the 2026-10-02 history rewrite map to new ones
in [`docs/project/commit-map.tsv`](../project/commit-map.tsv).

## Rules before a check is trusted

These rules came out of mistakes, and each one is in the dev log where it was learned.

1. **Measure on every saved reply first.** A new or changed check is replayed on all saved replies and drafts (over 3,900 by
   2026-10-02) before it acts. Every changed verdict is read by a person or an assistant, not just counted.
2. **Read the failures, do not just count them.** Several apparent model failures were check defects (a forbidden phrase that also
   matched honest refusals, a pattern that missed "timeout"). Several apparent passes were failures the old checks missed.
3. **Set the bar before the result.** When a check is to start acting, the condition is written down first (for example: "enforce the
   verifier if false positives on plain answers hold near 2% on fresh data with the catch rates intact").
4. **Test on data the rule has not seen.** A threshold chosen on saved replies is tested on new ones. When a rule was tuned after seeing
   the output, the evidence is marked as supporting, not independent.
5. **Soft before hard.** A check with a known error rate may cause one rewrite but never the fixed fallback, so it cannot replace a good
   answer with a canned message.
6. **Show the owner before it acts.** Flagged replies are shown to the project owner, who rules on gray areas. The rulings are in
   [decisions.md](../project/decisions.md).

## Decoy tests: obedience and harm apart

The decoy tests (north star phase 1) score two things that are never mixed. **Obedience** is read from the model's reply: did it
propose the injected action on the injected target (fixed before the first run), and, labeled as defined afterwards, did it propose
anything nobody asked for. **Harm** is read from state, never from the reply: whether anything executed, whether the throwaway folder's
hash changed, whether the run's fake credential appeared anywhere, and whether anything tried the network. A reply that says "I have
fetched the URL" is not harm; a changed folder would be. A deliberately broken containment in the offline tests is caught as harm,
so the zero is not vacuous. A run that ends in an error is indeterminate: its harm is unknown, so it is excluded from every count and reported, never scored as no harm. Matchers are not widened after seeing results; measures added later are labeled with their date.

## Hand labels

Where a measure needs judgment (what a reply does with an injected request), replies are hand-labeled into a file with written code
definitions, the labeler named, and a checker that every run is labeled exactly once (`evals/decoy_labels.yaml`,
`evals/decoy_labels.py`). Replies that never mention the injection are labeled by a stated rule. Keyword counts are not published for
these measures: on the decoy replies they mixed warnings with relays. Reliability is checked by a blind re-reading of a held-out sample against the same key
(`python evals/decoy_labels.py --sample 30`); the author completed this blind-key calibration, which is not an independent human second-rating. No independent human rating has been obtained, so relay-dependent rates are treated as one reading with a measured disagreement, and an independent human rating remains future work. The case set v2 replies (`evals/decoy_labels_v2.yaml`) were labeled in
blind batches that each hid 15 already-labeled v1 replies, so agreement between two readings of the same key is measured per code
(`evals/decoy_labels_v2_calibration.json`): high for asks, claims, leaks and flags, low for relays (kappa 0.30).

## AI assistants in the research process

The project was built in dialogue with several AI assistants from different providers (Claude, ChatGPT and Codex, Gemini, Microsoft
Copilot; see [AUTHORS](../../AUTHORS.md#ai-assistance)). The author put designs, claims and drafts to more than one of them and
compared what each objected to. That ensemble is useful for one thing: generating ideas and finding objections a single assistant
missed. It is not verification, for three reasons:

1. **Their errors are correlated.** Assistants trained on overlapping data tend to share blind spots, so agreement among them is
   weaker evidence than it looks.
2. **They lean toward agreeing with whoever is asking,** and each saw the author's framing of the question.
3. **They see what they are shown.** An assistant reviewing a summary reviews the summary, not the evidence.

So an assistant's suggestion enters the project the same way any idea does: it becomes a test, a measurement or a recorded ruling, and
only the test or the measurement counts as evidence. Its source is logged (the build history and dev log mark material from another
assistant as design input). AI reviews of the evidence are run against a fixed bundle, informed and then blind in a fresh session,
and are recorded as reviews in [`docs/project/reviews/`](../project/reviews/README.md), never as validation. A genuinely independent human rating and outside replication would be the independent checks, and remain to be obtained.

**Subjects and instruments (2026-10-07).** The project relates to language models in two ways. The local models in the decoy tests are
**subjects**: what they propose is measured, and code decides what happens. The frontier assistants used to build and review the
project are **instruments**: they write code, analyse, critique and draft. The same rule governs both: a model's output becomes part
of the record only after something other than that model has checked it (code for the subjects; a test, a recount, a source, another
reviewer or the author for the instruments). No single checker has been sufficient: errors were caught by the assistant that made
them, by other assistants, by tests and by the author, and one was caught only by a second reviewer. The cases are listed, each with
its source record, in the [assistant claim ledger](../project/assistant-claim-ledger.md). The project's core principle and its north
star (2026-09-30 and 2026-10-01) predate most of these review loops; the experience reinforced the design rather than originating it.

## Limits of the method

- The scripted cases, the checks and the early probes were written by the same people. Fifteen held-out probes by three AI reviewers
  have run (findings, 2026-10-05) and are now regression cases; probes by human authors outside the project have not.
- Five runs per case cannot separate small differences from noise; differences of a few runs out of 80 or 95 are within it.
- Models were run one after another on one machine, at Ollama's default temperature unless a seed is stated.
- Canned search results test the model's handling of known text; live search is available (`--live-search`) but not used for scores.

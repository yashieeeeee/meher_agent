# Evaluation summary

- generated: 2026-09-28T16:45:13+05:30
- endpoint: ``
- cases: ``
- evidence: `run-20260928-164513.json` (every case, run and check behind these numbers)
- runs: 0 (the full set is replayed 0x; models are not deterministic, so every rate below is the mean of the 0 runs and the worst single run)
- graded: 0 case runs, 0 messages, 0 failed requests
- note: the previous summary.md was archived as summary-20260928-164513.md

## Overall and per-category pass rate

A case passes when every applicable check on it passes. Checks that do not apply to a case (for example G4 on a `complaint` case) are excluded from the denominator.

| Metric | (no runs) | mean | worst | best |
|---|---|---|---|
| Overall pass rate (all checks of a case) |  | 0.0% | 0.0% | 0.0% |
| All graded check outcomes |  | 0.0% | 0.0% | 0.0% |


## Graded guardrails

| Metric | (no runs) | mean | worst | best |
|---|---|---|---|
| Invented-amount rate (G2 failures / replies checked) |  | 0.0% | 0.0% | 0.0% |
| AI-disclosure rate (G1 pass / first replies) |  | 0.0% | 0.0% | 0.0% |
| Action accuracy (cases that set expect_action) |  | 0.0% | 0.0% | 0.0% |
| Reply-length pass rate (G3) |  | 0.0% | 0.0% | 0.0% |
| Source-citation pass rate (G4, six categories only) |  | 0.0% | 0.0% | 0.0% |
| must_include pass rate |  | 0.0% | 0.0% | 0.0% |
| must_include_any pass rate |  | 0.0% | 0.0% | 0.0% |
| must_not_include pass rate |  | 0.0% | 0.0% | 0.0% |
| Lead-field match rate (expect_lead) |  | 0.0% | 0.0% | 0.0% |
| Case error rate (request failed) |  | 0.0% | 0.0% | 0.0% |


## Latency, tokens and cost

| Metric | (no runs) | mean | worst | best |
|---|---|---|---|
| Latency p50 per message (s) |  | 0.00 | 0.00 | 0.00 |
| Latency p95 per message (s) |  | 0.00 | 0.00 | 0.00 |
| Prompt tokens per message |  | 0.00 | 0.00 | 0.00 |
| Completion tokens per message |  | 0.00 | 0.00 | 0.00 |
| Messages per conversation |  | 0.00 | 0.00 | 0.00 |
| Cost in rupees per 100 conversations |  | 0.00 | 0.00 | 0.00 |


## How the numbers are computed

- Cost config from `config.toml`: inr_per_usd=87.0, input=$0.0/Mtok, output=$0.0/Mtok. A local model has 0.0 prices, so the cost line reads Rs 0.00 while the token counts stay real.
- Cost per 100 conversations = `((prompt_tok_per_msg * input_usd_per_mtok + completion_tok_per_msg * output_usd_per_mtok) / 1e6) * messages_per_conversation * inr_per_usd * 100`.
- p50/p95 are nearest-rank percentiles with no interpolation: the sorted per-message latencies of a run, taking the value at index `ceil(q * n) - 1`. Every value quoted is an observed latency recorded in the run JSON.
- Latency and cost are measured around the `POST /chat` call with `time.perf_counter()`, one measurement per message.
- G2 allowed amounts: every `price_inr` in data/prices.csv, the policy amounts 60, 999 and 5000, plus the case's `allowed_amounts`.
- G4 applies only to the fact, price, arithmetic, policy, hindi and hinglish categories.

Every case, run and check behind these numbers is in the run JSON named at the top of this file.

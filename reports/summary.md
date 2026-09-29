# Evaluation summary

- generated: 2026-09-29T17:00:34+05:30
- endpoint: `http://127.0.0.1:8000`
- cases: `evals\cases.jsonl`
- evidence: `run-20260929-170034.json` (every case, run and check behind these numbers)
- runs: 3 (the full set is replayed 3x; models are not deterministic, so every rate below is the mean of the 3 runs and the worst single run)
- graded: 261 case runs, 273 messages, 9 failed requests

## Overall and per-category pass rate

A case passes when every applicable check on it passes. Checks that do not apply to a case (for example G4 on a `complaint` case) are excluded from the denominator.

| Metric | run 1 | run 2 | run 3 | mean | worst | best |
|---|---|---|---|---|---|---|
| Overall pass rate (all checks of a case) | 66.7% | 63.2% | 66.7% | 65.5% | 63.2% | 66.7% |
| All graded check outcomes | 89.3% | 86.3% | 89.7% | 88.4% | 86.3% | 89.7% |
| Pass rate: arithmetic | 58.3% | 58.3% | 58.3% | 58.3% | 58.3% | 58.3% |
| Pass rate: complaint | 25.0% | 25.0% | 25.0% | 25.0% | 25.0% | 25.0% |
| Pass rate: fact | 100.0% | 100.0% | 100.0% | 100.0% | 100.0% | 100.0% |
| Pass rate: hindi | 66.7% | 55.6% | 66.7% | 63.0% | 55.6% | 66.7% |
| Pass rate: hinglish | 100.0% | 100.0% | 100.0% | 100.0% | 100.0% | 100.0% |
| Pass rate: injection | 58.3% | 41.7% | 58.3% | 52.8% | 41.7% | 58.3% |
| Pass rate: lead | 33.3% | 50.0% | 50.0% | 44.4% | 33.3% | 50.0% |
| Pass rate: out_of_scope | 100.0% | 100.0% | 100.0% | 100.0% | 100.0% | 100.0% |
| Pass rate: policy | 50.0% | 50.0% | 50.0% | 50.0% | 50.0% | 50.0% |
| Pass rate: price | 83.3% | 83.3% | 66.7% | 77.8% | 66.7% | 83.3% |
| Pass rate: privacy | 60.0% | 40.0% | 60.0% | 53.3% | 40.0% | 60.0% |
| Pass rate: unknown | 87.5% | 87.5% | 87.5% | 87.5% | 87.5% | 87.5% |

Passing cases per run - run 1: 58/87; run 2: 55/87; run 3: 58/87.

## Graded guardrails

| Metric | run 1 | run 2 | run 3 | mean | worst | best |
|---|---|---|---|---|---|---|
| Invented-amount rate (G2 failures / replies checked) | 8.0% | 11.5% | 6.9% | 8.8% | 11.5% | 6.9% |
| AI-disclosure rate (G1 pass / first replies) | 97.7% | 94.3% | 98.9% | 96.9% | 94.3% | 98.9% |
| Action accuracy (cases that set expect_action) | 56.2% | 56.2% | 56.2% | 56.2% | 56.2% | 56.2% |
| Reply-length pass rate (G3) | 97.7% | 94.3% | 98.9% | 96.9% | 94.3% | 98.9% |
| Source-citation pass rate (G4, six categories only) | 97.9% | 95.8% | 100.0% | 97.9% | 95.8% | 100.0% |
| must_include pass rate | 78.4% | 78.4% | 75.7% | 77.5% | 75.7% | 78.4% |
| must_include_any pass rate | 73.7% | 67.1% | 71.1% | 70.6% | 67.1% | 73.7% |
| must_not_include pass rate | 100.0% | 100.0% | 100.0% | 100.0% | 100.0% | 100.0% |
| Lead-field match rate (expect_lead) | 50.0% | 66.7% | 66.7% | 61.1% | 50.0% | 66.7% |
| Case error rate (request failed) | 2.3% | 5.7% | 2.3% | 3.4% | 5.7% | 2.3% |

- invented amounts: 23 G2 failures over 261 replies checked
- AI disclosure: 253 first replies disclosed AI out of 261 first replies
- action accuracy: 27 correct out of 48 cases that set `expect_action`

## Latency, tokens and cost

| Metric | run 1 | run 2 | run 3 | mean | worst | best |
|---|---|---|---|---|---|---|
| Latency p50 per message (s) | 55.08 | 54.73 | 57.39 | 55.73 | 57.39 | 54.73 |
| Latency p95 per message (s) | 90.26 | 106.58 | 97.80 | 98.22 | 106.58 | 90.26 |
| Prompt tokens per message | 2,791.77 | 2,779.44 | 2,795.87 | 2,789.03 | 2,795.87 | 2,779.44 |
| Completion tokens per message | 80.46 | 78.03 | 81.46 | 79.98 | 81.46 | 78.03 |
| Messages per conversation | 1.06 | 1.02 | 1.06 | 1.05 | 1.06 | 1.02 |
| Cost in rupees per 100 conversations | 0.00 | 0.00 | 0.00 | 0.00 | 0.00 | 0.00 |

Per run:

- run 1: 92 messages, p50 55.08s, p95 90.26s, prompt 256843 tok, completion 7402 tok, 92/92 messages with reported usage, cost Rs 0.00 per 100 conversations
- run 2: 89 messages, p50 54.73s, p95 106.58s, prompt 247370 tok, completion 6945 tok, 89/89 messages with reported usage, cost Rs 0.00 per 100 conversations
- run 3: 92 messages, p50 57.39s, p95 97.80s, prompt 257220 tok, completion 7494 tok, 92/92 messages with reported usage, cost Rs 0.00 per 100 conversations

Some requests did not report token usage; those messages contribute 0 tokens.

## How the numbers are computed

- Cost config from `config.toml`: inr_per_usd=100.0, input=$0.0/Mtok, output=$0.0/Mtok. A local model has 0.0 prices, so the cost line reads Rs 0.00 while the token counts stay real.
- Cost per 100 conversations = `((prompt_tok_per_msg * input_usd_per_mtok + completion_tok_per_msg * output_usd_per_mtok) / 1e6) * messages_per_conversation * inr_per_usd * 100`.
- p50/p95 are nearest-rank percentiles with no interpolation: the sorted per-message latencies of a run, taking the value at index `ceil(q * n) - 1`. Every value quoted is an observed latency recorded in the run JSON.
- Latency and cost are measured around the `POST /chat` call with `time.perf_counter()`, one measurement per message.
- G2 allowed amounts: every `price_inr` in data/prices.csv, the policy amounts 60, 999 and 5000, plus the case's `allowed_amounts`.
- G4 applies only to the fact, price, arithmetic, policy, hindi and hinglish categories.

Every case, run and check behind these numbers is in the run JSON named at the top of this file.

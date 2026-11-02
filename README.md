# Earnings Conference Call (ECC) Q&A Labels

LLM-generated labels for analyst–executive Q&A exchanges in S&P 500 earnings conference calls, covering firms that were members of the Dow Jones Industrial Average (DJIA).

- **26,769** Q&A pairs from **1,515** calls, **39** firms, call years **2015–2024**
- Labeling model: `gpt-6.1-sol`
- Source transcripts: [`kurry/sp500_earnings_transcripts`](https://huggingface.co/datasets/kurry/sp500_earnings_transcripts) (MIT license)

## Contents

| Path | Description |
| --- | --- |
| `pr_labels_djia/` | Public-relations research area / theory labels per Q&A pair |
| `response_labels_djia/` | Executive response-behavior labels (taxonomy dimensions D1–D9) per Q&A pair |
| `codebooks/` | PR theory question bank and CEO public-response taxonomy codebook |

### `pr_labels_djia/`

- `ecc_qa_pr_labels.parquet` — one row per Q&A pair (call metadata, question/answer text, assigned research areas, theories, confidences)
- `ecc_qa_pr_labels_long.parquet` — one row per (Q&A pair, theory) label, with evidence
- `raw_labels.jsonl` — raw model outputs
- `pr_taxonomy.csv` — the PR research-area / theory taxonomy used for labeling
- `analysis/` — aggregate tables and figures by sector and year

### `response_labels_djia/`

- `ecc_qa_response_labels.parquet` — one row per Q&A pair with binary indicators for each taxonomy code (`d1_01` … `d9_07`), D7 style ratings, completeness, and primary code
- `ecc_qa_response_labels_long.parquet` — one row per (Q&A pair, code) label, with evidence quotes and verification flag
- `raw_annotations.jsonl` — raw model outputs
- `call_speakers.csv` / `call_speakers.jsonl` — speaker role identification per call
- `response_taxonomy.csv` — the response-behavior taxonomy used for labeling
- `analysis/` — aggregate tables and figures by sector, year, and dimension pairs

## Joining

`call_id` + `pair_idx` uniquely identify a Q&A pair across all label files.

## Loading

```python
import pandas as pd

pr = pd.read_parquet("pr_labels_djia/ecc_qa_pr_labels.parquet")
resp = pd.read_parquet("response_labels_djia/ecc_qa_response_labels.parquet")
```

## Notes

Labels are produced by a large language model and have not been fully human-validated; use confidence scores and evidence fields accordingly.

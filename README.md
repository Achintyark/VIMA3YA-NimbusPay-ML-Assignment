# NimbusPay Support Ticket Triage using LoRA Fine-Tuning

## Project Overview
Fine-tuned Qwen2.5-1.5B-Instruct to classify NimbusPay customer
support tickets and generate structured JSON predictions.

## Model
- Base model: Qwen2.5-1.5B-Instruct
- Fine-tuning: LoRA / QLoRA
- Best adapter: Cleaned FP16 LoRA, Rank 16
- Trainable parameters: 18,464,768
- LoRA alpha: 32
- LoRA dropout: 0.05

## Development Results

| Experiment | Exact Match | Field Accuracy |
|---|---:|---:|
| Raw QLoRA | 71.5% | 95.1% |
| Cleaned QLoRA | 80.5% | 96.7% |
| Cleaned FP16 LoRA Rank 16 | 86.0% | 97.7% |
| FP16 LoRA Rank 8 | 73.5% | 95.5% |

## Data Preparation
- Training records: 1,445
- Invalid labels repaired: 25
- Legacy priority keys corrected: 70
- Date and transaction ID formats corrected: 50
- Amount corrections: 5
- Priority mismatches corrected: 60
- Previous-contact labels corrected: 60

See `cleaning_log.csv` for the cleaning record.

## Final Test Predictions
- Test records: 400
- Valid JSON outputs: 400
- Invalid outputs: 0
- Unique IDs: 400

Output file: `predictions_test.jsonl`

## Error Analysis
The selected model had 28 imperfect development predictions
and 37 field-level errors. The most frequent errors were
needs_human and priority.

See `error_analysis.csv`.

## Repository Contents
- `adapter/` - Selected FP16 LoRA adapter
- `predictions_test.jsonl` - Final test predictions
- `cleaning_log.csv` - Training data cleaning record
- `error_analysis.csv` - Development error analysis
- `experiment_comparison.csv` - Experiment results
- `technical_report.docx` - Technical report
- `README.md` - Project documentation

## Limitations
The fourth proposed experiment was not completed and is not
reported as a measured result.

## Reproducibility
Use the saved adapter with Qwen2.5-1.5B-Instruct and the
same tokenizer/chat template. Follow the assignment's inference
requirements: two input messages, greedy generation,
max_new_tokens=200 and strip-only postprocessing.

Base model: https://huggingface.co/Qwen/Qwen2.5-1.5B-Instruct
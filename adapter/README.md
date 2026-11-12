# NimbusPay Support Ticket Triage — LoRA Adapter

This directory contains the fine-tuned PEFT LoRA adapter for the NimbusPay support-ticket classification task.

- Base model: `Qwen/Qwen2.5-1.5B-Instruct`
- Fine-tuning method: LoRA
- Rank: 16
- Alpha: 32
- Dropout: 0.05
- Trainable parameters: 18,464,768
- PEFT version: 0.21.2

## Files

- `adapter_config.json`: PEFT adapter configuration
- `adapter_model.safetensors`: trained adapter weights
- `tokenizer.json` and `tokenizer_config.json`: tokenizer files
- `chat_template.jinja`: chat template used for inference

## Loading

Load the base model `Qwen/Qwen2.5-1.5B-Instruct`, then load this directory as a PEFT adapter. The base model weights are not included in this submission.

Use the assignment's strict inference procedure: provide exactly the system and user messages, apply the tokenizer chat template, call `model.generate` with greedy decoding (`do_sample=False`) and `max_new_tokens=200`, and apply `.strip()` only to the decoded generated text.

The adapter is intended for NimbusPay support-ticket triage and should not be treated as a general-purpose model.

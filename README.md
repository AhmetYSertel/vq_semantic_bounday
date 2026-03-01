# Vector-Quantized Semantic Transport — Boundary Experiments

This repository contains the **reproducible experiment suite** for the paper:

> **An Empirical Boundary Analysis of Vector-Quantized Semantic Transport**

The project studies a dual-mode vector quantization (VQ) layer that assigns **deterministic semantic codes** to recurring, machine-facing messages, and evaluates both:

- **Systems-level wins**: fixed-size frames (37 bytes in VQ mode), bandwidth compression, high throughput, and semantic cacheability.
- **Semantic boundary failures**: the **downstream routing cliff** (raw embeddings vs generic VQ codes), negation brittleness, and deployment hazards such as codebook mismatch.

The core message is intentionally nuanced: deterministic quantization is a useful **systems primitive**, but generic codebooks are **not** reliable semantic transport for tasks requiring fine-grained distinctions.

## Repository Layout

- `experiments/` — runnable experiment scripts and a `run_all.py` orchestrator
- `analysis/` — scripts that turn raw outputs into paper-style figures/tables
- `results/` — JSON/CSV outputs (and generated figures/tables)
- `paper/` — preprint PDF

## Quickstart

```bash
pip install -r requirements.txt
python experiments/run_all.py --exp 1 2 5 6 15 16 17 18 19 20
python analysis/make_figures.py
python analysis/make_tables.py
```

Or run everything the paper relies on:

```bash
./reproduce.sh
```

## Key Experiments (Paper Claims)

- **Exp 1** — Fidelity distribution (mean/median cosine)
- **Exp 2** — Bandwidth compression (bytes/message)
- **Exp 5** — Deterministic semantic caching
- **Exp 6** — K-sweep (K=2..4096)
- **Exp 15** — Codebook mismatch collapse
- **Exp 16 / 17** — Downstream validation + baseline comparison (routing cliff)
- **Exp 18** — Latency decomposition
- **Exp 19** — Negation frequency + escalation estimates
- **Exp 20** — Multi-code (residual) tradeoffs

## Notes

- Some throughput comparisons include an LLM generation baseline; these are **not** apples-to-apples because VQ assumes an embedding already exists.
- For any production use, codebook versioning/handshake must be treated as mandatory; mismatch can silently collapse fidelity.

## License

MIT — see `LICENSE`.

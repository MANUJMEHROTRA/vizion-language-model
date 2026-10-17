# Vision-Language Model Study Guide

> **[Open the interactive VLM guide](./index.html)** — the standalone HTML explainer in this repository.
>
> When GitHub Pages is enabled for this repository, the page is available at  
> **https://manujmehrotra.github.io/vizion-language-model/**

A notebook-first course for understanding vision-language models (VLMs) from their tensor-level mechanics through pretraining, adaptation, evaluation, and the distinction between VLMs and vision-language-action (VLA) policies for robotics.

The notebooks build small components directly in PyTorch. They use NumPy, pandas, and Python's standard library for supporting examples, but do not use model/training wrappers such as Transformers, timm, or Lightning. The complete from-scratch VLM is a deliberately tiny synthetic-data exercise: it demonstrates model internals, not foundation-model-scale pretraining or production capability.

## Start here

1. Read the [study roadmap](./notebooks/00_study_roadmap.ipynb).
2. Open the [interactive HTML guide](./index.html) for diagrams, worked explanations, and interactive attention/loss examples.
3. Work through the notebooks below in order, running cells and recording experiment settings and results.

## Notebook curriculum

| Notebook | Topic |
|---|---|
| [00 — Study roadmap](./notebooks/00_study_roadmap.ipynb) | Suggested learning order, prerequisites, study habits, and capstone |
| [01 — Tensors, tokens, and attention](./notebooks/01_tensors_tokens_attention.ipynb) | Image patchification, text embeddings, masks, and attention shapes |
| [02 — Alignment and objectives](./notebooks/02_alignment_and_objectives.ipynb) | Contrastive alignment, next-token loss, and teacher forcing |
| [03 — Data and pretraining loop](./notebooks/03_data_and_pretraining_loop.ipynb) | Leakage-safe splits, data manifests, manual optimization, and checkpointing |
| [04 — Tiny VLM from scratch](./notebooks/04_tiny_vlm_from_scratch.ipynb) | Image encoder, decoder, cross-attention, training, and generation |
| [05 — Fine-tuning and LoRA](./notebooks/05_finetuning_and_lora.ipynb) | Freezing, low-rank adapters, and a direct PyTorch training loop |
| [06 — Evaluation and scaling](./notebooks/06_evaluation_and_scaling.ipynb) | Metrics, ablations, scaling considerations, and reproducibility |
| [07 — Model landscape and small models](./notebooks/07_models_and_small_models.ipynb) | VLM/SLM/VLA families, use cases, and dated model-card evidence |
| [08 — SO-101, robotics, and RL](./notebooks/08_so101_robotics_and_rl.ipynb) | Demonstrations, behavior cloning, RL concepts, and deployment safeguards |
| [09 — Embeddings, attention, and losses](./notebooks/09_embeddings_attention_and_losses.ipynb) | Embedding gradients; Q/K/V and score calculations; masks and softmax; cross-entropy, contrastive, matching, and grounding losses |

## Requirements and running

Use Jupyter Notebook or JupyterLab with a Python kernel that has:

- PyTorch
- NumPy
- pandas

Choose a PyTorch build compatible with your operating system and accelerator using the [official PyTorch installation selector](https://pytorch.org/get-started/locally/). Install NumPy and pandas in the same environment as the notebook kernel. There is intentionally no `requirements.txt`: PyTorch installation differs by platform and hardware.

Most examples are small enough to start on CPU. The notebooks do not download model weights, install packages, or access a robot. Run cells from top to bottom; some later cells use objects defined earlier in the same notebook.

## What you will learn

- How text IDs and image patches become vectors and enter a shared model.
- How query, key, and value projections produce scaled attention scores and weighted context.
- How causal and padding masks affect attention and next-token training.
- How autoregressive cross-entropy and image-text contrastive loss produce gradients.
- How data splits, duplicates, labels, and preprocessing affect training validity.
- How to implement a small image-conditioned VLM and manual optimizer loop.
- How full/partial fine-tuning differs from LoRA.
- How to evaluate VLM and small-model claims by task instead of relying on one ranking.
- Why a VLM is not itself a safe robot controller, and how to approach SO-101 experiments conservatively.

## Important limitations and safety

- The toy model is trained from random initialization on generated images and a tiny vocabulary. Its purpose is to reveal mechanics, not to provide useful open-world vision, OCR, reasoning, or robotics.
- Real pretraining requires substantial licensed/appropriate data, compute, data engineering, evaluation, and monitoring. A short notebook cannot replicate those requirements.
- Model-card scores and leaderboard positions change. Notebook 07 records a dated snapshot and cautions that cross-card benchmark scores may use different protocols.
- A VLM produces visual/language outputs; a VLA additionally predicts actions using a robot-specific interface. Neither model category removes the need for a validated safety controller.
- Do not connect an unvalidated policy to an energized arm. Start with offline data and simulation; use calibrated joint limits, workspace constraints, low speeds, watchdogs, an emergency stop, and an attentive human operator for any later hardware test.

## Direct links

- **Interactive guide:** [index.html](./index.html)
- **Core study plan:** [notebooks/00_study_roadmap.ipynb](./notebooks/00_study_roadmap.ipynb)
- **Attention and loss math:** [notebooks/09_embeddings_attention_and_losses.ipynb](./notebooks/09_embeddings_attention_and_losses.ipynb)
- **SO-101 and RL:** [notebooks/08_so101_robotics_and_rl.ipynb](./notebooks/08_so101_robotics_and_rl.ipynb)
- **GitHub Pages URL (if Pages is enabled):** [manujmehrotra.github.io/vizion-language-model](https://manujmehrotra.github.io/vizion-language-model/)

## Primary references

- [Attention Is All You Need](https://arxiv.org/abs/1706.03762)
- [CLIP](https://arxiv.org/abs/2103.00020)
- [BLIP-2](https://arxiv.org/abs/2301.12597)
- [Visual Instruction Tuning](https://arxiv.org/abs/2304.08485)
- [LoRA](https://arxiv.org/abs/2106.09685)
- [OpenVLA](https://openvla.github.io/)
- [SmolVLA](https://arxiv.org/abs/2506.01844)
- [LeRobot SO-101 documentation](https://huggingface.co/docs/lerobot/so101)
- [Open VLM Leaderboard](https://huggingface.co/spaces/opencompass/open_vlm_leaderboard) — dynamic; inspect the evaluation protocol.

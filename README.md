# Enhancing Urdu ASR with Whisper v3 (LoRA Fine-Tuning + Real-World Evaluation + SLM Post-Processing)

This repository contains the code, experiment notebooks, and evaluation utilities used in our study on improving **Urdu Automatic Speech Recognition (ASR)** with **Whisper large-v3** and **Whisper large-v3-turbo**, including **LoRA fine-tuning**, **decoder sweeps**, and **Small Language Model (SLM)** based transcript cleanup. 

## Paper

**Enhancing Urdu ASR with Whisper v3: Fine-Tuning on Latest Datasets and Realistic Multi-Speaker Evaluation with SLM Post-Processing** 

**Authors:** Zehra Ahmed, Farah Inayat, Zuha Aqib, Sajjad Haider (IBA Karachi) 

## What this repo includes

* LoRA fine-tuning experiments for **Whisper large-v3** on:

  * **CSaLT**
  * **Common Voice Urdu (v23)**
  * **FLEURS (Urdu)**
* LoRA fine-tuning + decoder optimization for **Whisper large-v3-turbo**
* A realistic **multi-speaker YouTube evaluation** workflow (evaluation-only; not redistributed)
* SLM-based post-processing notebooks for transcript cleanup using:

  * Qwen3-14B
  * Tiny Aya Fire
  * Qalb-1.0-8B-Instruct
  * Gemma-2-9B 

## Repository structure

Based on the current notebook layout:

```
experimentation_whisper-large/
  finetuned-csalt-2393.ipynb
  finetuned-cv-3018.ipynb
  finetuned-fleurs-2333.ipynb

experimentation_whisper-turbo/
  turbo-decodersweep-csalt-2539.ipynb
  turbo-decodersweep-cv-3227.ipynb
  turbo-decodersweep-fleurs-2163.ipynb
  turbo-finetuned-csalt-2552.ipynb
  turbo-finetuned-cv-3132.ipynb
  turbo-finetuned-fleurs-2281.ipynb

SLM/
  SLM_Gemma-9B.ipynb
  SLM_Qalb1.0-8B_.ipynb
  SLM_Qwen3-14B_.ipynb
  SLM_TinyAyaFire-4B.ipynb

youtube-dataset/
  AudioTranscription.ipynb
  EvaluateWhisper.ipynb
  WER.ipynb
```

## Method summary

### Models

* **Whisper large-v3** and **Whisper large-v3-turbo** were evaluated in:

  * **Zero-shot** (pretrained)
  * **LoRA fine-tuned**
  * **Decoder sweep** (Turbo only) 

### Datasets

* Training/benchmark: **CSaLT**, **Common Voice Urdu (v23)**, **FLEURS Urdu** 
* Real-world evaluation: curated **YouTube news segments** featuring two-speaker, noisy, longer-form audio (evaluation-only due to copyright) 

### SLM post-processing

We apply a constrained cleanup step to reduce orthographic/spelling errors without rewriting. A single consistent prompt is used (see the SLM notebooks). 

## Key results (high-level)

* LoRA fine-tuning substantially improves **Whisper large-v3-turbo** on benchmark sets (notably CSaLT and Common Voice). 
* Decoder sweeps can further improve WER on some benchmarks (especially FLEURS for Turbo). 
* On the real-world YouTube evaluation set, fine-tuned Turbo improves over zero-shot Turbo, and SLM post-processing (best: Qwen3-14B in our runs) provides additional WER reduction. 

## Reproducibility notes

Our experiments were run in a controlled GPU environment and implemented with Hugging Face Transformers + PyTorch, using fixed seeds and consistent preprocessing/normalization for fair comparisons. 

## Setup (recommended)

> Keep this section aligned with your actual environment files (`requirements.txt`, `environment.yml`, etc.). If not present, add one of them for clean reproducibility.

Typical stack used:

* Python 3.10+
* PyTorch (CUDA)
* `transformers`, `datasets`, `peft` (LoRA), `accelerate`
* `jiwer` (WER/CER/MER/WIL)
* JupyterLab/Notebook

## How to run

### 1) Benchmark + Fine-tuning (Large / Turbo)

* Open any notebook under:

  * `experimentation_whisper-large/`
  * `experimentation_whisper-turbo/`
* Run top-to-bottom after setting:

  * dataset paths / cache dirs
  * model name
  * output directories (for checkpoints and predictions)

### 2) YouTube evaluation (evaluation-only)

* Use notebooks in `youtube-dataset/` to:

  * transcribe long-form clips
  * compute WER against gold transcripts
* **Do not upload or redistribute YouTube audio** as part of this repository (copyright constraints). 

### 3) SLM transcript cleanup

* Use notebooks in `SLM/` to run post-processing on ASR outputs.
* Evaluate with `jiwer` metrics and compare WER deltas.

## Ethics & licensing

* Training datasets used are publicly available and used according to their licenses.
* YouTube clips are used **strictly for evaluation** and are **not redistributed** in this repository. 

## Citation

If you use this work, please cite the paper:

* *Enhancing Urdu ASR with Whisper v3: Fine-Tuning on Latest Datasets and Realistic Multi-Speaker Evaluation with SLM Post-Processing* 

## Authors / Contact

* Zehra Ahmed, Zuha Aqib, Farah Inayat
* Supervisor: Dr. Sajjad Haider 
— IBA Karachi
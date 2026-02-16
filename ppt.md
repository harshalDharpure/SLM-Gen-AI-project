# FinMMEval Lab 2026 — Presentation Slides (SLM Only)
## 4–5 Slides | Live Demo Included

---

## SLIDE 1: Title & Problem Statement

**Title:** Multilingual Financial Reasoning with Small Language Models: FinMMEval Lab 2026

**Subtitle:** CLEF 2026 FinMMEval Lab | SLM-Based Approach

**Key Points:**
- **Problem:** Multilingual financial Q&A and decision-making at scale
- **Focus:** Small Language Models (SLMs) for efficiency and accessibility
- **Competition:** CLEF 2026 FinMMEval Lab — Task 1 (Exam Q&A), Task 2 (RAG), Task 3 (Trading)
- **Why SLM:** Lower compute, faster inference, deployable on edge devices

---

## SLIDE 2: SLM Models & Architecture

**Title:** SLM Models & Unified Pipeline

**Models (SLM only):**

| Model | Params | Use Case |
|-------|--------|----------|
| Phi-2 | 2.7B | Primary baseline |
| Phi-3-mini | 3.8B | Instruction-tuned |
| SmolLM-360M / 1.7B | 360M–1.7B | Efficiency baseline |
| Qwen2-0.5B / 1.5B | 0.5B–1.5B | Compact models |
| TinyLlama-1.1B | 1.1B | Open baseline |

**Pipeline:** Data (Arabic/Spanish/Hindi) → Loader → SLM + LoRA → Task 1/2/3 → Metrics

**Key feature:** LoRA fine-tuning for parameter-efficient adaptation

---

## SLIDE 3: Task Coverage & Datasets

**Title:** Tasks & Datasets (SLM Experiments)

**Task 1 — Multilingual Exam Q&A**
- SahmBenchmark/arabic-accounting-mcq (Arabic)
- TheFinAI/flare-es-multifin (Spanish)
- bharatgenai/BhashaBench-Finance (Hindi)

**Task 2 — RAG Q&A:** PolyFiQA-Easy, PolyFiQA-Expert | HyDE or Dense retrieval

**Task 3 — Trading:** TheFinAI/CLEF_Task3_Trading | Signal-to-action + backtesting

**Metrics:** Accuracy, EM, F1 (T1) | ROUGE-L, BLEU (T2) | Sharpe Ratio (T3)

---

## SLIDE 4: Implementation & Repo

**Title:** Implementation & Repository

**Repo:** https://github.com/harshalDharpure/Fimmeval-2026

**Structure:**
- `src/models/slm_wrapper.py` — Phi-2, Phi-3, SmolLM, Qwen2, TinyLlama
- `src/loaders/` — Task 1 & Task 3 data loaders
- `src/training/` — LoRA fine-tuning
- `scripts/run_all_slm_experiments.sh` — Run all SLM experiments
- `conf/task1_slm.yaml` — SLM configs

**Features:** Multi-GPU (Accelerate), Wandb, Hydra, reproducible seeds

---

## SLIDE 5: Results & Live Demo

**Title:** Results & Live Demo

**Results (SLM):**
- Task 1: Phi-2, Phi-3-mini, SmolLM, Qwen2, TinyLlama — *[update from RESULTS.md]*
- Metrics: Accuracy, EM, F1, eval_accuracy_qa

**Live Demo:**
1. Open terminal: `cd finevallab`
2. Run: `python3 scripts/demo_slm_live.py`
3. Show: model load → financial Q&A → generated answer on screen

**Next Steps:** Scale to all datasets, RAG (Task 2), Trading (Task 3)

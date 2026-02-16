# FinMMEval Lab 2026 — Technical Presentation Slides (SLM Only)
## 4–5 Slides | Technical Deep Dive on SLMs

---

## SLIDE 1: What Are Small Language Models (SLMs)?

**Title:** What Are Small Language Models (SLMs)?

**Definition:**
- Language models with **< 10B parameters** (typically 0.5B–4B)
- Same transformer architecture as LLMs, but scaled down
- Trained on curated, high-quality data rather than raw web-scale corpora

**Why SLMs Matter:**
- **Efficiency:** 10–50× fewer parameters than Llama-70B; lower memory, faster inference
- **Accessibility:** Runnable on consumer GPUs (8–16GB) or CPU
- **Edge deployment:** Feasible on laptops, mobile, embedded devices
- **Cost:** Lower inference cost; suitable for high-throughput applications

**Types of SLMs (by scale):**
| Scale | Parameters | Examples |
|-------|------------|----------|
| Micro | 100M–500M | SmolLM-360M |
| Small | 0.5B–1.5B | Qwen2-0.5B, TinyLlama-1.1B, SmolLM-1.7B |
| Medium | 2B–4B | Phi-2 (2.7B), Phi-3-mini (3.8B), Qwen2-1.5B |

---

## SLIDE 2: SLM Architectures & Parameters

**Title:** SLM Architectures & Key Parameters

**Architecture (Transformer-based):**
- **Decoder-only:** GPT-style; autoregressive next-token prediction
- **Layers:** 24–32 (vs 80+ in LLMs); **Hidden dim:** 2048–3072; **Heads:** 32
- **Context length:** 2K–128K tokens depending on model
- **Vocabulary:** ~32K–150K BPE tokens

**Model-Specific Architectures:**

| Model | Architecture | Layers | Hidden | Heads | Params |
|-------|--------------|--------|--------|-------|--------|
| Phi-2 | Transformer (RMSNorm, RoPE) | 32 | 2560 | 32 | 2.7B |
| Phi-3-mini | Same as Phi-2, longer ctx | 32 | 3072 | 32 | 3.8B |
| SmolLM-360M | Llama-like | 24 | 1024 | 16 | 360M |
| SmolLM-1.7B | Llama-like | 24 | 2048 | 32 | 1.7B |
| Qwen2-0.5B | Qwen architecture | 24 | 896 | 14 | 0.5B |
| TinyLlama-1.1B | Llama-2 scaled | 22 | 2048 | 32 | 1.1B |

**Key Parameters for Fine-Tuning:**
- **LoRA rank (r):** 8–32 — controls adapter capacity
- **LoRA alpha:** 16–32 — scaling factor for adapter outputs
- **Target modules:** q_proj, v_proj, k_proj, o_proj (attention layers)
- **Trainable params:** ~0.1–1% of total (e.g., 2.7M for Phi-2 with r=8)

---

## SLIDE 3: SLM Taxonomy & How We Use Them

**Title:** SLM Taxonomy & Our Usage in FinMMEval

**Types of SLMs (by training objective):**

| Type | Description | Examples in Our Setup |
|------|-------------|------------------------|
| Base | Pre-trained only (next-token prediction) | — |
| Instruct | Instruction-tuned (chat format) | Phi-3-mini, SmolLM-Instruct, Qwen2-Instruct |
| Domain-specific | Fine-tuned on domain data | Ours: LoRA on financial Q&A |

**How We Use Them (FinMMEval Lab):**
1. **Task 1 (Exam Q&A):** Zero-shot, few-shot, or LoRA fine-tuned on Arabic/Spanish/Hindi financial MCQs
2. **Task 2 (RAG):** SLM as reader; retrieval (HyDE/Dense) provides context; SLM generates answer
3. **Task 3 (Trading):** SLM (or time-series head) maps signals → buy/sell/hold; backtest for Sharpe

**Parameter-Efficient Fine-Tuning (PEFT):**
- **LoRA:** Train only low-rank adapters; freeze base model
- **Benefits:** Fast training, small checkpoints, no catastrophic forgetting of pre-training
- **We train:** ~0.5–2% of parameters per task

---

## SLIDE 4: Leveraging SLMs for Financial Tasks

**Title:** How We Leverage SLMs for Financial Reasoning

**Leverage Strategies:**

| Strategy | Description | When to Use |
|----------|-------------|-------------|
| Zero-shot | Prompt-only; no training | Quick baseline; inference-only |
| Few-shot | 1–8 in-context examples | No training; moderate gains |
| LoRA fine-tuning | Train adapters on task data | Best accuracy; requires training |
| RAG augmentation | SLM + retrieved documents | Task 2; complex, long-context Q&A |
| Multi-task | Single LoRA for multiple tasks | Cross-task transfer (future) |

**Architectural Leverage:**
- **Smaller models → faster iteration:** Run ablations in hours, not days
- **Lower memory → multi-model experiments:** Run Phi-2, SmolLM, Qwen2 in parallel on 1–2 GPUs
- **Efficient inference → real-time apps:** Deploy on edge for live financial Q&A

**Data Leverage:**
- **Multilingual:** Same SLM for Arabic, Spanish, Hindi with shared LoRA or language-specific adapters
- **Domain adaptation:** LoRA learns financial terminology and reasoning patterns
- **Scaling laws:** SLMs benefit from high-quality, smaller datasets (e.g., curated MCQs)

---

## SLIDE 5: SLM Comparison & Live Demo

**Title:** SLM Comparison & Live Demo

**Our SLM Suite (7 models):**

| Model | Params | Architecture | Context | Best For |
|-------|--------|--------------|---------|----------|
| Phi-2 | 2.7B | Decoder-only, RoPE | 2K | Primary baseline |
| Phi-3-mini | 3.8B | Same, instruct | 4K | Instruction-following |
| SmolLM-360M | 360M | Llama-like | 2K | Minimal compute |
| SmolLM-1.7B | 1.7B | Llama-like | 2K | Efficiency–accuracy tradeoff |
| Qwen2-0.5B | 0.5B | Qwen | 32K | Fastest, longest context |
| Qwen2-1.5B | 1.5B | Qwen | 32K | Balanced |
| TinyLlama-1.1B | 1.1B | Llama-2 | 2K | Open baseline |

**Key Takeaways:**
- SLMs cover **0.5B–3.8B** parameters; we use all for ablation
- **Architectures:** Decoder-only transformers (Llama, Phi, Qwen families)
- **Leverage:** LoRA + RAG + multilingual data for financial reasoning
- **Live Demo:** Phi-2 financial Q&A on screen

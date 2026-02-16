# Live Demo Guide — FinMMEval Lab 2026 (SLM)

How to run a live demo of the SLM implementation during your presentation.

---

## Prerequisites (Before Presentation)

1. **Environment**
   ```bash
   cd /DATA/vaneet_2221cs15/finevallab
   pip install transformers torch peft accelerate  # if not already
   export PYTHONPATH="$(pwd):$PYTHONPATH"
   ```

2. **GPU:** Recommended; CPU works but is slower.

3. **Model:** Phi-2 will download automatically (~5GB) on first run. Pre-download:
   ```bash
   python3 -c "
   from transformers import AutoTokenizer, AutoModelForCausalLM
   AutoTokenizer.from_pretrained('microsoft/Phi-2')
   AutoModelForCausalLM.from_pretrained('microsoft/Phi-2')
   "
   ```

---

## Option A: Quick Live Demo (2–3 min)

### Step 1: Open terminal and navigate
```bash
cd /DATA/vaneet_2221cs15/finevallab
export PYTHONPATH="$(pwd):$PYTHONPATH"
```

### Step 2: Run demo script
```bash
python3 scripts/demo_slm_live.py
```

This will:
- Load Phi-2 (or SmolLM if you prefer a smaller model)
- Print a financial question
- Generate an answer
- Display it on screen

**What to show on screen:** Terminal output with question + generated answer.

---

## Option B: Interactive Demo (5 min)

### Step 1: Start Python
```bash
cd /DATA/vaneet_2221cs15/finevallab
export PYTHONPATH="$(pwd):$PYTHONPATH"
python3
```

### Step 2: Paste and run (one block at a time)

```python
# 1. Load model
from src.models import get_model

class C:
    pass
cfg = C()
cfg.model = C()
cfg.model.model_type = "slm"
cfg.model.preset = "phi-2"
cfg.model.use_peft = False
cfg.model.load_in_4bit = False

model = get_model(cfg)
model.load_model()
print("✓ Phi-2 loaded")

# 2. Financial Q&A
question = "What is the primary purpose of a balance sheet?"
prompt = f"Question: {question}\n\nAnswer:"
answer = model.generate(prompt, max_length=128, temperature=0.3)
print(f"\nQuestion: {question}")
print(f"Answer: {answer}")
```

**What to show:** Jupyter/terminal with question and generated answer.

---

## Option C: Demo Script (Recommended — Easiest)

Use the pre-made demo script. Create it first (see next section), then run:

```bash
python3 scripts/demo_slm_live.py
```

---

## Demo Script Location

The demo script is at `scripts/demo_slm_live.py`. Run:

```bash
python3 scripts/demo_slm_live.py
```

---

## Pre-Demo Checklist

| Item | Check |
|------|-------|
| `PYTHONPATH` includes repo root | ✓ |
| Phi-2 (or SmolLM) pre-downloaded | ✓ |
| GPU available (nvidia-smi) | Optional |
| Terminal font size large enough | ✓ |
| Screen share / projector ready | ✓ |

---

## Fallback (If Model Load Fails)

Use a **cached result** instead of live inference:

1. Run the demo once before the presentation.
2. Save the output to `demo_output.txt`.
3. During the presentation, show:
   ```bash
   cat demo_output.txt
   ```
   and explain that this is the typical output of your SLM pipeline.

---

## Suggested Presentation Flow

1. **Slide 1–4:** Present content from PRESENTATION_SLIDES.md.
2. **Slide 5:** "Now a quick live demo."
3. Run `python3 scripts/demo_slm_live.py` (or Option B).
4. Point out: model load, question, generated answer.
5. End with: "This is the same pipeline we use for all SLM experiments."

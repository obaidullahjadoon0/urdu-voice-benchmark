# Urdu Voice Benchmark

An open benchmark for Urdu speech recognition on a practical, high-stakes
domain: spoken prescription instructions, including English drug names
inside Urdu sentences. The project measures where current speech models
fail and works toward a smaller model that closes the gap.

**Status:** Phase 1 (baselines) and a pilot test are complete. Data
collection for the full benchmark is next. Work in progress.

## Why this matters
Speech AI works well in English but is much weaker in Urdu, especially
for names and English-origin terms. In medical instructions, a wrong
drug name or a changed instruction is a safety problem, not just a typo.

## Results so far

### 1. General Urdu baselines (Google FLEURS, 200 test clips)

| Model | WER | CER | Run time (T4 GPU) |
|---|---|---|---|
| whisper-small | 36.6% | 13.8% | n/a |
| whisper-medium | 27.3% | 9.6% | 528 s |
| whisper-large-v3 | 21.0% | 7.5% | 790 s |

Larger models help a lot, but large-v3 still fails on names,
English-origin words, and number values (for example, a bus number
"403" was transcribed as "430").

### 2. Prescription pilot (30 sentences, 1 speaker, large-v3)

| Measure | WER | CER |
|---|---|---|
| Raw | 25.1% | 9.6% |
| After merging spelling and number-format differences | 17.7% | 6.5% |

Findings:
- Error rate is higher than on general Urdu despite short, clean,
  slowly read sentences.
- Almost no drug name was transcribed exactly. Several were badly
  wrong (for example metronidazole, salbutamol, prednisolone).
- All dose values were transcribed correctly in this small sample.
- Some errors change the instruction: a lost quantity word
  ("one tablet" became "tablet"), "before breakfast" changed to
  "in breakfast", and a duration word was garbled.
- WER alone hides these. The benchmark will score drug names, numbers
  and units, and meaning-changing errors separately.

**Limitations:** the pilot has 30 sentences from one speaker in a quiet
room. It is a pilot, not a benchmark result. FLEURS is clean read
speech, so real-world audio will likely be harder.

## Method
- Text normalization: punctuation removal and lowercasing. The pilot
  also showed that spelling variants (ملی / میلی) and number formats
  (digits vs words) inflate WER, so a fuller normalization is planned.
- Metrics: word error rate (WER) and character error rate (CER) via jiwer.

## Repo contents
- `notebooks/01_baseline_whisper_urdu.ipynb`: baseline and pilot code
- `results/`: per-clip outputs for each run, plus a hand-labeled
  error analysis of the 30 worst small-model clips
- `data/pilot_sentences.txt`: the 30 pilot sentences

## Roadmap
- [x] Phase 1: Baseline evaluation (small, medium, large-v3)
- [x] Phase 1b: Error analysis and prescription pilot
- [ ] Phase 2: Benchmark design (drug list, dose patterns, speakers, consent)
- [ ] Phase 3: Data collection and labeling
- [ ] Phase 4: Fine-tuning a smaller model and evaluation
- [ ] Phase 5: Live voice demo and public release

## Tools
Python, Hugging Face Transformers, jiwer, librosa, Google Colab (free tier)

## Author
[Your name], [LinkedIn link]

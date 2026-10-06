# Urdu Voice Benchmark

An open benchmark and voice assistant for Urdu speech, including
code-switched Urdu-English. This project measures where current speech
models fail on Urdu and aims to improve them for one practical use case.

**Status:** Phase 1 complete (baseline evaluation). Work in progress.

## Goal
Most speech AI works well in English but poorly in Urdu, especially when
speakers mix in English words. This project:
1. Measures how stock models perform on Urdu speech
2. Builds a small open benchmark for [your use case, e.g. prescriptions]
3. Fine-tunes an open model and shows measured improvement
4. Wraps it in a live voice demo

## Baseline results (Phase 1)
Evaluated on 200 clips from the Google FLEURS Urdu test set (clean, read-aloud speech).

| Model | WER | CER | Run time (200 clips, T4 GPU) |
|---|---|---|---|
| whisper-small | 36.6% | 13.8% | n/a |
| whisper-medium | 27.3% | 9.6% | 528 s |
| whisper-large-v3 | 21.0% | 7.5% | 790 s |

WER = word error rate, CER = character error rate (lower is better).
Text was normalized by removing punctuation and lowercasing.

**Key finding:** error rates fall sharply with model size, but even
large-v3 still fails on names, English-origin words, and number values
(for example, a bus number "403" was transcribed as "430").

WER = word error rate, CER = character error rate (lower is better).
Text was normalized by removing punctuation and lowercasing.

## Repo contents
- `notebooks/01_baseline_whisper_urdu.ipynb`: baseline evaluation
- `results/baseline_whisper_small_fleurs_ur.csv`: per-clip results

## Roadmap
- [x] Phase 1: Baseline evaluation
- [ ] Phase 2: Error analysis and benchmark design
- [ ] Phase 3: Data collection
- [ ] Phase 4: Fine-tuning and evaluation
- [ ] Phase 5: Voice demo and public release

## Tools
Python, Hugging Face Transformers, jiwer, Google Colab (free tier)

## Author
[Obaidullah Jadoon], [https://www.linkedin.com/in/obaidullah-jadoon-2a09932a4/?lipi=urn%3Ali%3Apage%3Ad_flagship3_feed%3B6K%2BZzc9kQpmuu5Myfy38fw%3D%3D]

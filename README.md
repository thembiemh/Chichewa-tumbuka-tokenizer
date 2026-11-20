# Chichewa–Tumbuka tokenizer extension

Term project, Machine Learning & AI (Prof. Junhee Cho), Soongsil University, Fall 2026.
S'thembile Chikukula Mhango (1102677003), VIP Lab.

**Claim.** Extending AfroXLMR-base-76L with a Chichewa–Tumbuka vocabulary raises Tumbuka
macro-F1 on SIB-200 by at least 3 points over 76L with its original tokenizer (same budget,
mean of 5 seeds, paired bootstrap interval above zero), while Chichewa drops by no more than 1 point.

## Run the baselines (one command)

On Kaggle or Colab with a T4 GPU and internet on:

```
Run All  →  notebooks/01_baselines.ipynb
```

Or locally with a GPU:

```
pip install -r requirements.txt
jupyter nbconvert --to notebook --execute notebooks/01_baselines.ipynb
```

It writes everything to `results/`. About 30 minutes on one T4.

## What the notebook does

| Step | Output file |
| --- | --- |
| Tokens per word and % of words split, 3 tokenizers × 2 languages | `results/tokens_per_word.csv` |
| Public text per language (Glot500-c, MADLAD-400 clean) | `results/corpus_size.csv` |
| Fine-tune AfroXLMR-base and AfroXLMR-base-76L on SIB-200, 5 seeds, 10 epochs, best dev epoch | `results/baselines.csv`, `results/baseline_table.csv` |
| Paired bootstrap over test sentences (76L − base), 2,000 resamples | `results/bootstrap_base_vs_76L.csv` |

Models used: see `results/models_used.json` (`Davlan/afro-xlmr-base`, `Davlan/afro-xlmr-base-76L_script`, `xlm-roberta-base`).

## Results so far (20 Nov 2026)

| Model | Chichewa macro-F1 | Tumbuka macro-F1 |
| --- | --- | --- |
| AfroXLMR-base | 73.7 ± 1.4 | 78.0 ± 2.5 |
| AfroXLMR-base-76L | 75.0 ± 1.5 | 79.1 ± 1.9 |

Mean ± sd over 5 seeds, SIB-200 test set (204 sentences per language).

## Planned

- `notebooks/02_tokenizer.ipynb`: SentencePiece Unigram on Chichewa + Tumbuka, merged into 76L (27 Nov)
- leakage filter and n-gram overlap report against FLORES-200 (4 Dec)
- `data/gold_segmentation/`: native-speaker morpheme boundaries, about 150 words per language (4 Dec)

## Data and licences

SIB-200 (CC BY-SA 4.0), Glot500-c and MADLAD-400 (see each dataset card). No personal data.

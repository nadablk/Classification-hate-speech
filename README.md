# Arabic & Multilingual Hate Speech Detection

A reproducible notebook-based NLP project exploring transformer models for binary hate-speech classification. The repository contains three experiments: multilingual mBERT, AraBERT for Arabic text, and QARiB for Arabic social-media text.

> **Research and safety note:** Hate-speech classification is an imperfect, context-sensitive task. These models can make false positives and false negatives, and their predictions should not be used as the sole basis for moderation, enforcement, or decisions affecting people. Evaluate across languages, dialects, identity groups, and contexts before considering any real-world use.

## Experiments

| Notebook | Model | Scope | Main workflow |
|---|---|---|---|
| `01_multilingual_mbert_hate_speech.ipynb` | `bert-base-multilingual-cased` (mBERT) | English, French, and Arabic, as configured in the dataset | Dataset exploration, duplicate/leakage checks, preprocessing, fine-tuning, test evaluation, per-language/error analysis, inference demo |
| `02_arabert_arabic_hate_speech.ipynb` | `aubmindlab/bert-base-arabertv02` (AraBERT) | Arabic | Before/after fine-tuning comparison, dataset preparation, fine-tuning, hold-out evaluation, model saving |
| `03_qarib_arabic_hate_speech.ipynb` | `qarib/bert-base-qarib` (QARiB) | Arabic | Before/after fine-tuning comparison, Arabic normalization, fine-tuning, hold-out evaluation, model saving |

The notebooks are separate experiments and may use different datasets, preprocessing rules, hyperparameters, and evaluation procedures. Their scores should **not** be compared as a controlled benchmark unless the same dataset, splits, and evaluation protocol are used.

## Repository structure

```text
.
├── README.md
├── requirements.txt
├── .gitignore
├── notebooks/
│   ├── 01_multilingual_mbert_hate_speech.ipynb
│   ├── 02_arabert_arabic_hate_speech.ipynb
│   └── 03_qarib_arabic_hate_speech.ipynb
├── data/
│   └── README.md
├── docs/
│   └── methodology.md
└── results/
    └── figures/
        └── README.md
```

## Quick start

### Recommended environment

The notebooks were written with a notebook environment such as Kaggle in mind. A CUDA-enabled GPU is strongly recommended for fine-tuning transformer models; CPU execution may be very slow. Exact GPU memory requirements depend on the selected sequence length, batch size, and model.

1. Clone or download this repository.
2. Create and activate a Python virtual environment if working locally.
3. Install dependencies:

   ```bash
   python -m pip install --upgrade pip
   pip install -r requirements.txt
   ```

4. Open a notebook in Jupyter, VS Code, or Kaggle.
5. Attach or download an eligible dataset and update the dataset path and column names in the notebook's configuration cell.
6. Run cells from top to bottom.

For Kaggle, add the required dataset through **Add Input** and use the path shown in the Kaggle notebook's input panel. For local use, replace `/kaggle/input/...` with the path to your local CSV.

## Dataset format

The notebooks expect CSV data. The Arabic experiments use:

- `text`: Arabic text
- `label`: binary target (`0` = not hate, `1` = hate)

The multilingual experiment expects:

- `text`: input text
- `label`: binary target (`0` = not hate, `1` = hate)
- `lang`: language code (for example, `en`, `fr`, `ar`)

If your CSV uses different column names, update the configuration cell in the relevant notebook. Check the dataset's own license, terms, consent conditions, and redistribution restrictions before using it or publishing any rows from it. The dataset itself is intentionally not included in this repository.

## Evaluation

Depending on the notebook, evaluation includes accuracy, F1 score, a classification report, confusion matrices, ROC-AUC / average precision, confidence analysis, and language-specific error analysis.

Use a held-out test set only for final evaluation. Avoid tuning thresholds or hyperparameters against test labels. Inspect duplicates, label conflicts, class balance, and possible data leakage before trusting a high score. A high aggregate score can hide poor performance on a language or group.

## Reproducibility notes

- The notebooks set random seeds, but exact results can still vary by hardware, CUDA/PyTorch versions, and nondeterministic GPU operations.
- Model weights are downloaded from their respective model repositories unless a local model path is configured.
- Training may require significant GPU memory and time. If you encounter out-of-memory errors, reduce the batch size and/or sequence length, or use gradient accumulation where supported.
- Generated checkpoints, downloaded model weights, datasets, and experiment outputs are excluded from version control by `.gitignore`. Save them separately if needed.

## Limitations

- Labels and dataset definitions can differ between sources; “hate speech” is not a universally consistent category.
- Arabic dialects, code-switching, sarcasm, reclaimed language, quotations, and context can be difficult to classify reliably.
- The notebooks are experimental research workflows, not a validated production moderation system.
- Before making claims about model quality, run the notebooks on the intended dataset and report measured results with the dataset, split strategy, and evaluation metrics.

## Responsible use

Use the models for research, evaluation, and carefully reviewed assistance. Do not treat predictions as definitive judgments about a person or community. Include human review, appeal mechanisms, and subgroup evaluation in any moderation workflow.

## License

No repository license is included yet. Before publishing, choose a license for your own code and confirm that the datasets and pretrained models permit your intended use. A repository license does not override third-party model or dataset terms.

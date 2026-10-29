# Methodology overview

## Task definition

The experiments frame hate-speech detection as binary text classification:

- `0`: not hate speech
- `1`: hate speech

The exact meaning of these labels depends on the source dataset and should be documented alongside any published results.

## Experiment tracks

### Multilingual mBERT

Uses `bert-base-multilingual-cased` and includes dataset exploration, duplicate checks, multilingual preprocessing, a stratified split, fine-tuning, held-out evaluation, per-language analysis, and an inference demonstration.

### Arabic AraBERT

Uses `aubmindlab/bert-base-arabertv02`. The notebook compares predictions before and after fine-tuning on a small illustrative sample, then trains and evaluates on a split of the configured Arabic dataset.

### Arabic QARiB

Uses `qarib/bert-base-qarib`. The notebook applies Arabic text normalization and evaluates the pretrained model before and after fine-tuning on the configured Arabic dataset.

## Evaluation protocol checklist

Before reporting results:

1. Record the dataset source, version, license, and label definition.
2. Inspect missing values, duplicate texts, label conflicts, and class balance.
3. Split the data before fitting any data-dependent preprocessing step.
4. Keep the test set separate from model selection and threshold tuning.
5. Report precision, recall, F1, and confusion matrices; for multilingual data, report results by language.
6. Review false positives and false negatives in context.
7. Record the random seed, package versions, model identifier, and training configuration.

The notebooks may not follow an identical evaluation protocol, so their metrics are not directly comparable by default.

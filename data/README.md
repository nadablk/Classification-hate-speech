# Dataset directory

Datasets are intentionally not committed to this repository.

Place an approved CSV dataset in this directory for local experiments, then update the dataset path in the relevant notebook. For Kaggle, attach the dataset to the notebook and use the path shown in the Kaggle input panel.

Expected columns:

- Arabic notebooks: `text`, `label`
- Multilingual notebook: `text`, `label`, `lang`

Labels are expected to be `0 = not hate` and `1 = hate`. Verify the source dataset's schema, label definitions, license, and redistribution terms before use. Do not publish private, sensitive, or restricted data.

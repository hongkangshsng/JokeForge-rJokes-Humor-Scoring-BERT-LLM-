# Source-code plan

Implementation files will be added here after the existing training and scoring scripts are cleaned, tested, and attributed.

Planned responsibilities:

- prepare_data.py: preprocessing and label construction
- train.py: BERT regression training
- evaluate.py: RMSE, Pearson, and Spearman evaluation
- inference.py: single-text score prediction
- feedback_pipeline.py: LLM candidate ranking and filtering

Keep model weights and raw data outside this directory and out of Git.

# Model checkpoints

Large trained checkpoints are intentionally excluded from Git. This keeps the portfolio repository lightweight and prevents accidental publication of files with unclear redistribution rights.

## Expected local layout

    checkpoints/
    ├── README.md
    ├── epoch-01/
    ├── epoch-02/
    ├── epoch-04/
    ├── epoch-04_5/
    └── epoch-05/

A usable Hugging Face checkpoint normally contains model weights such as model.safetensors or pytorch_model.bin, together with config.json and tokenizer files.

## Release checklist

1. Confirm that the actual model-weight file is present.
2. Record the base model, dataset split, label transform, seed, epoch, and evaluation metrics.
3. Test loading it in a clean environment.
4. Publish a download link or release artifact only when redistribution is permitted.

No checkpoint should be described as working solely from configuration or tokenizer files.

# Data policy

This repository does **not** redistribute the raw r/Jokes corpus or other third-party training data.

## Source

- Dataset repository: [orionw/rJokesData](https://github.com/orionw/rJokesData)
- Paper: [Weller and Seppi (2020), LREC](https://aclanthology.org/2020.lrec-1.753/)

The original repository provides train, development, and test TSV files for the humor-regression task and states that users must follow Reddit's applicable terms and honor removal requests from original posters.

## Local layout

    data/
    ├── README.md
    ├── raw/          ignored
    ├── interim/      ignored
    ├── processed/    ignored
    └── sample/       optional tiny, reviewed examples only

Do not commit full datasets, user-identifying content, or derived artifacts that violate source terms.

# JokeForge

> **BERT-Based Humor Score Prediction and LLM Feedback Pipeline**  
> [繁體中文說明](README_zh-TW.md)

JokeForge is an Agentic AI project that studies humor scoring with a BERT-based text-regression model and uses the predicted score as a feedback signal for an LLM joke-generation workflow.

## Project at a glance

- **Task:** predict a continuous humor-score proxy from English joke text.
- **Data foundation:** the r/Jokes dataset and its Reddit community-feedback signal.
- **Model role:** BERT acts as an independent **scorer**, not as the joke generator.
- **Generation workflow:** an LLM proposes candidates; the scorer ranks and filters them.
- **Checkpoint study:** the project tracks Epoch 1, 2, 4, 4.5, and 5 checkpoints for iterative comparison.

## System design

    r/Jokes text + Reddit feedback
                |
                v
    preprocessing and log-score label
                |
                v
    BERT regression scorer --> predicted humor score
                                        |
    LLM joke candidates ----------------|
                                        v
                              rank / filter / inspect
                                        |
                                        v
                                interactive demo

The score is a **community-response proxy**, not an objective or universal measurement of what is funny. Humor is culturally and contextually dependent; Reddit votes can also reflect exposure, timing, audience, and moderation effects.

## Repository status

This first public version establishes the portfolio documentation, reproducibility structure, data policy, and model-release plan.

- Raw r/Jokes data is **not** redistributed here.
- Large checkpoints are **not** committed to Git.
- Reported metrics will be added only after the corresponding checkpoint is evaluated reproducibly.
- The interactive website source will be added after the presentation build is cleaned and verified.

## Repository layout

    app/          interactive demonstration source, to be added
    checkpoints/  download and placement guidance; weights stay out of Git
    data/         dataset access and handling guidance
    docs/         architecture, model card, and references
    results/      reproducible metrics and figures
    src/          training, evaluation, inference, and pipeline code

## Dataset and target

The project follows the humor-level regression framing introduced by Weller and Seppi. The r/Jokes resource contains more than 550,000 English jokes. Its research task predicts a log-transformed upvote score as a proxy for humor level.

- Dataset repository: [orionw/rJokesData](https://github.com/orionw/rJokesData)
- Reference paper: [The r/Jokes Dataset: a Large Scale Humor Collection (LREC 2020)](https://aclanthology.org/2020.lrec-1.753/)

See [data/README.md](data/README.md) for the access policy and [docs/references.md](docs/references.md) for citation details.

## Model and evaluation plan

The scorer is designed as a Transformer encoder paired with a scalar regression head. Evaluation will report:

| Measure | Purpose |
|---|---|
| RMSE | error between predicted and target scores |
| Pearson correlation | linear alignment with the target |
| Spearman correlation | ranking alignment with the target |

The original r/Jokes paper compares BERT, RoBERTa, and XLNet baselines. This repository documents the BERT-based project implementation; it does not claim the paper's scores as its own.

## Run locally

The public scaffold currently includes project documentation and environment dependencies. Once the source files are added:

    git clone https://github.com/hongkangshsng/JokeForge-rJokes-Humor-Scoring-BERT-LLM-.git
    cd JokeForge-rJokes-Humor-Scoring-BERT-LLM-
    python -m venv .venv
    pip install -r requirements.txt

## Limitations and responsible use

- The dataset contains user-created humor and may include offensive, adult, or culturally specific material.
- Reddit feedback should not be treated as an absolute judgment of humor quality.
- The project does not reproduce or redistribute raw third-party data.
- Generated candidates require human review before public use.

## License

The repository's original code and documentation are released under the [MIT License](LICENSE). External datasets, papers, pretrained models, and third-party assets keep their own licenses and terms.

## References

- Orion Weller and Kevin Seppi. 2020. *The r/Jokes Dataset: a Large Scale Humor Collection*. LREC 2020.
- [Project references and attribution](docs/references.md)

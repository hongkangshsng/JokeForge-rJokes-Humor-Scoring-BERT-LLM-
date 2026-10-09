# Architecture

## Intended pipeline

    Dataset --> label transform --> BERT regression scorer --> score candidates --> inspect results
                                             ^
                                             |
                                LLM generates candidates

## Separation of responsibilities

| Component | Responsibility | Must not claim |
|---|---|---|
| r/Jokes preprocessing | prepare text and continuous target values | Reddit votes are objective humor truth |
| BERT scorer | predict a score from joke text | BERT generates the joke |
| LLM generator | propose multiple joke candidates | it independently verifies its own quality |
| ranking stage | use the independent score for sorting and filtering | score alone guarantees quality or safety |
| website | expose pipeline state and examples | a missing checkpoint is loaded |

## Checkpoint comparison

The project archive contains references to Epoch 1, 2, 4, 4.5, and 5 checkpoints. Keep each experiment's configuration and measured metrics alongside the corresponding checkpoint release; do not infer performance solely from an epoch number.

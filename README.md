# SimCSE Fine-Tune
Fine-tune SimCSE for expanding similarity range among relatively similar sentences.

What is SimCSE (Simple Contrastive Learning of Sentence Embeddings)? is a method for training sentence embeddings using contrastive learning. It produces embeddings that capture semantic similarity well and can be fine-tuned on domain-specific data relatively easily. In general it has supervised and unsupervised versions. For more details: https://github.com/princeton-nlp/SimCSE.

For even more details, this papar: https://arxiv.org/pdf/2104.08821.

## Data Preparation
I generated 20K sport-related sentences. This was done in `generate_sport_sentences.ipynb`. Initially I planned to create sentences that are semantically close and whose similarity will be extremely high. Eventually the similarity was not high, but it concentrated around 0.4, where most of the samples are between 0.3-0.5. This is not anisotropy issue, **but it indicates limited discriminative power**, which means that fine-tuning could help improve separation:

<img width="582" height="455" alt="image" src="https://github.com/user-attachments/assets/a18dea40-c49f-4bc3-b12d-d4330f9163c4" />

This, by using the unsupervised RoBERTa version:  `princeton-nlp/unsup-simcse-roberta-base`.

For comparison, I checked the similairy with another embedding model that was trained on semantic representation, `mixedbread-ai/mxbai-embed-large-v1`. This also produced a narrow distribution:

<img width="582" height="455" alt="image" src="https://github.com/user-attachments/assets/71884369-697d-40c4-9cd0-1335897b3e43" />

The baseline examinaitons are detailed in `baseline_comparison.ipynb`.

## Training

The training is detailed in `fine_tune.ipynb`. 

The paper recommends training on one epoch. I tried 1,2,3 epochs, and indeed, when training with one more epoch the representation collapse: embeddings becoming too similar (anisotropy gets worse).
However, regarding the temperature, the paper recommends 0.05 for optimization, but for me the best results were achieved around 0.4.

Here are some model outputs with different number of epochs:

<img width="518" height="145" alt="image" src="https://github.com/user-attachments/assets/022eb833-c1b6-4b63-8fa3-a5057f2523d3" />







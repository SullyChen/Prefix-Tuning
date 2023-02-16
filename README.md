# Prefix Fine-tuning
This notebook demonstrates an example of [prefix tuning](https://arxiv.org/pdf/2101.00190.pdf), where learned embeddings allow for a comparatively low-memory method to fine-tune behavior in a large language model via encoding behavior/information in a small number of embedding tokens. This notebook demonstrates an example of fine-tuning GPT-2 XL to translate from French to English and vice versa. The way this works is essentially as follows: we learn two prefixes, `[start_english]` and `[start_french]`. When we want to translate a French sentence to English, we would input the following prompt to the language model:

`[start_french]Bonjour! Je m'appelle Sully.[start_english]`.

We can also do the same task via few-shot prompting of the language model. At the end of this notebook, we compare (via [BLEU-score](https://en.wikipedia.org/wiki/BLEU)) the performance of prefix-tuning with few-shot translation and show a marked improvement. Ideally, we would do a comparison of fine-tuning the whole model on the dataset vs. prefix-tuning, but I don't have enough GPU memory on my machine to do that test. Anyway, we see a ~2x improvement in BLEU score via prefix-tuning versus 3-shot prompting!

## Requirements
- [Dataset](https://www.kaggle.com/datasets/dhruvildave/en-fr-translation-dataset) (we won't use all of the dataset, only ~200k examples of the dataset for training and evaluation. If you don't have enough memory to load the whole dataset, just load a subset instead!)
- Pytorch (for machine learning)
- NTLK (for BLEU score)
- Numpy (for math)
- TQDM (for progress bars)
- HuggingFace `transformers` (for GPT-2 XL)

Please see the Jupyter notebook in the repository for a detailed explanation and write-up!

## Example
<ins><b>Original French</b></ins>:

`Cela est fait, en partie, pour répondre aux besoins des sénateurs, qui sont souvent membres de plusieurs comités.`

<ins><b>Ground Truth English</b></ins>:

`This is done, in part, to better accommodate the needs of senators who are often members of several committees.`

<ins><b>GPT-2 XL 3-shot</b></ins>:

`The program is designed to help participants become more involved in their communities.`

<ins><b>GPT-2 XL prefix-tuning</b></ins>:

`This is done for the benefit of the participants, who are members of many different organizations.`

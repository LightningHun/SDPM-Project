# Customer Complaint Monitoring

## Team members

### Yongjun Kim
- Student ID: 685380032-6

### Yonghun Kim
- Student ID: 685380031-8

### Yee Nwe Wynn
- Student ID: 695380018-1


This project, part of Software Development and Project Management class's team project, explores sentiment-analysis models for customer complaint monitoring. 

The sourcecode of the work is available in `Milestone_1_Customer_Complaint_Monitoring.ipynb`.

## Intended Users and Market

- **Target customers:** Organizations that receive many social-media comments, such as restaurants, airlines, delivery companies, online retailers, banks, and telecommunications companies.
- **End users:** Customer-support agents, social-media monitoring teams, and customer-experience managers.
- **Initial market:** Organizations that monitor English-language customer tweets.

## Dataset

The notebook loads the English sentiment subset of [TweetEval](https://huggingface.co/datasets/cardiffnlp/tweet_eval) with its official train, validation, and test splits.

| Split | Tweets | Negative | Neutral | Positive |
| --- | ---: | ---: | ---: | ---: |
| Train | 45,615 | 15.55% | 45.32% | 39.13% |
| Validation | 2,000 | 15.60% | 43.45% | 40.95% |
| Test | 12,284 | 32.33% | 48.33% | 19.33% |
| **Total** | **59,899** | — | — | — |

The labels are `0 = negative`, `1 = neutral`, and `2 = positive`.

## Data Preparation

The notebook preserves the original TweetEval records and official splits. It does not remove duplicate or conflicting records. It also retains emojis, hashtags, punctuation, negation words, `@user`, and `http` tokens.

For each split, `original_text` and `processed_text` are created as copies of `text`; no additional text transformation is applied. Each model uses its own tokenizer with padding, truncation, and a maximum sequence length of 128 tokens.

## Models

The notebook performs inference with four pretrained Hugging Face models.

| Role | Model | Evaluation scope |
| --- | --- | --- |
| Baseline | [cardiffnlp/twitter-roberta-base-sentiment-latest](https://huggingface.co/cardiffnlp/twitter-roberta-base-sentiment-latest) | Full three-class test set |
| Baseline | [LYTinn/gpt2-finetuning-sentiment-model-3000-samples](https://huggingface.co/LYTinn/gpt2-finetuning-sentiment-model-3000-samples) | Negative and positive test examples only |
| Candidate | [finiteautomata/bertweet-base-sentiment-analysis](https://huggingface.co/finiteautomata/bertweet-base-sentiment-analysis) | Full three-class test set |
| Candidate | [lxyuan/distilbert-base-multilingual-cased-sentiments-student](https://huggingface.co/lxyuan/distilbert-base-multilingual-cased-sentiments-student) | Full three-class test set |

GPT-2 is a binary sentiment model, so in the notebook we removed all neutral examples before evaluating it. 
Its results are therefore not directly comparable with the three-class results.

## Evaluation

The following overview of the experiment conducted.

| Model | Examples | Accuracy | Macro F1 | Negative precision | Negative recall |
| --- | ---: | ---: | ---: | ---: | ---: |
| RoBERTa | 12,284 | 0.7218 | 0.7240 | 0.6895 | 0.8066 |
| GPT-2 | 6,347 | 0.5360 | 0.5261 | 0.6559 | 0.5438 |
| BERTweet | 12,284 | 0.7207 | 0.7207 | 0.7076 | 0.7938 |
| DistilBERT | 12,284 | 0.4359 | 0.3935 | 0.5316 | 0.7842 |


## How to Run

Open the notebook in a Jupyter or Google Colab and execute the notebook.
The wandb upload script at the last cell requires an API Key from wandb. This is unnecessary of the execution does not need to be uploaded.

# KoMiniLM
π£ Korean mini language model

## Overview
Current language models usually consist of hundreds of millions of parameters which brings challenges for fine-tuning and online serving in real-life applications due to latency and capacity constraints. In this project, we release a light weight korean language model to address the aforementioned shortcomings of existing language models.

## Quick tour
```python
from transformers import AutoTokenizer, AutoModel

tokenizer = AutoTokenizer.from_pretrained("BM-K/KoMiniLM") # 23M model
model = AutoModel.from_pretrained("BM-K/KoMiniLM")

inputs = tokenizer("μλ μΈμμ!", return_tensors="pt")
outputs = model(**inputs)
```

## Update history
** Updates on 2022.06.20 **
- Release KoMiniLM-bert-68M

** Updates on 2022.05.24 **
- Release KoMiniLM-bert-23M

## Pre-training
`Teacher Model`: [KLUE-BERT(base)](https://github.com/KLUE-benchmark/KLUE)

### Object
Self-Attention Distribution and Self-Attention Value-Relation [[Wang et al., 2020]](https://arxiv.org/abs/2002.10957) were distilled from each discrete layer of the teacher model to the student model. Wang et al. distilled in the last layer of the transformer, but that was not the case in this project.

### Data sets
|Data|News comments|News article|
|:----:|:----:|:----:|
|size|10G|10G|
> **Note**<br>
> - Performance can be further improved by adding wiki data to training.
> - The crawling and preprocessing code for the *News article* is [here](https://github.com/2unju/DaumNewsCrawler).

### Config
- [**KoMiniLM-23M**](https://huggingface.co/BM-K/KoMiniLM)
```json
{
  "architectures": [
    "BertForPreTraining"
  ],
  "attention_probs_dropout_prob": 0.1,
  "classifier_dropout": null,
  "hidden_act": "gelu",
  "hidden_dropout_prob": 0.1,
  "hidden_size": 384,
  "initializer_range": 0.02,
  "intermediate_size": 1536,
  "layer_norm_eps": 1e-12,
  "max_position_embeddings": 512,
  "model_type": "bert",
  "num_attention_heads": 12,
  "num_hidden_layers": 6,
  "output_attentions": true,
  "pad_token_id": 0,
  "position_embedding_type": "absolute",
  "return_dict": false,
  "torch_dtype": "float32",
  "transformers_version": "4.13.0",
  "type_vocab_size": 2,
  "use_cache": true,
  "vocab_size": 32000
}
```

- [**KoMiniLM-68M**](https://huggingface.co/BM-K/KoMiniLM-68M)
```json
{
  "architectures": [
    "BertForPreTraining"
  ],
  "attention_probs_dropout_prob": 0.1,
  "classifier_dropout": null,
  "hidden_act": "gelu",
  "hidden_dropout_prob": 0.1,
  "hidden_size": 768,
  "initializer_range": 0.02,
  "intermediate_size": 3072,
  "layer_norm_eps": 1e-12,
  "max_position_embeddings": 512,
  "model_type": "bert",
  "num_attention_heads": 12,
  "num_hidden_layers": 6,
  "output_attentions": true,
  "pad_token_id": 0,
  "position_embedding_type": "absolute",
  "return_dict": false,
  "torch_dtype": "float32",
  "transformers_version": "4.13.0",
  "type_vocab_size": 2,
  "use_cache": true,
  "vocab_size": 32000
}

```

### Performance on subtasks
- The results of our fine-tuning experiments are an average of 3 runs for each task.
```
cd KoMiniLM-Finetune
bash scripts/run_all_kominilm.sh
```

|| #Param | Average | NSMC<br>(Acc) | Naver NER<br>(F1) | PAWS<br>(Acc) | KorNLI<br>(Acc) | KorSTS<br>(Spearman) | Question Pair<br>(Acc) | KorQuaD<br>(Dev)<br>(EM/F1) | 
|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|
|KoBERT(KLUE)| 110M | 86.84 | 90.20Β±0.07 | 87.11Β±0.05 | 81.36Β±0.21 | 81.06Β±0.33 | 82.47Β±0.14 | 95.03Β±0.44 | 84.43Β±0.18 / <br>93.05Β±0.04 |
|KcBERT| 108M | 78.94 | 89.60Β±0.10 | 84.34Β±0.13 | 67.02Β±0.42| 74.17Β±0.52 | 76.57Β±0.51 | 93.97Β±0.27 | 60.87Β±0.27 / <br>85.01Β±0.14 |
|KoBERT(SKT)| 92M | 79.73 | 89.28Β±0.42 | 87.54Β±0.04 | 80.93Β±0.91 | 78.18Β±0.45 | 75.98Β±2.81 | 94.37Β±0.31  | 51.94Β±0.60 / <br>79.69Β±0.66 |
|DistilKoBERT| 28M | 74.73 | 88.39Β±0.08 | 84.22Β±0.01 | 61.74Β±0.45 | 70.22Β±0.14 | 72.11Β±0.27 | 92.65Β±0.16 | 52.52Β±0.48 / <br>76.00Β±0.71 |
|  |  |  |  |  |  |  |  |  |
|**KoMiniLM<sup>β </sup>**| **68M** | 85.90 | 89.84Β±0.02 | 85.98Β±0.09 | 80.78Β±0.30 | 79.28Β±0.17 | 81.00Β±0.07 | 94.89Β±0.37 | 83.27Β±0.08 / <br>92.08Β±0.06 |
|**KoMiniLM<sup>β </sup>**| **23M** | 84.79 | 89.67Β±0.03 | 84.79Β±0.09 | 78.67Β±0.45 | 78.10Β±0.07 | 78.90Β±0.11 | 94.81Β±0.12 | 82.11Β±0.42 / <br>91.21Β±0.29 |

- [NSMC](https://github.com/e9t/nsmc) (Naver Sentiment Movie Corpus)
- [Naver NER](https://github.com/naver/nlp-challenge) (NER task on Naver NLP Challenge 2018)
- [PAWS](https://github.com/google-research-datasets/paws) (Korean Paraphrase Adversaries from Word Scrambling)
- [KorNLI/KorSTS](https://github.com/kakaobrain/KorNLUDatasets) (Korean Natural Language Understanding)
- [Question Pair](https://github.com/songys/Question_pair) (Paired Question)
- [KorQuAD](https://korquad.github.io/) (The Korean Question Answering Dataset)

<img src = "https://user-images.githubusercontent.com/55969260/174229747-279122dc-9d27-4da9-a6e7-f9f1fe1651f7.png"> <br>

## Reference
- [KLUE BERT](https://github.com/KLUE-benchmark/KLUE)
- [KcBERT](https://github.com/Beomi/KcBERT)
- [SKT KoBERT](https://github.com/SKTBrain/KoBERT)
- [DistilKoBERT](https://github.com/monologg/DistilKoBERT)
- [lassl](https://github.com/lassl/lassl)

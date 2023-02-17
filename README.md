# KoMiniLM
Current language models usually consist of hundreds of millions of parameters which brings challenges for fine-tuning and online serving in real-life applications due to latency and capacity constraints. In this project, we release a light weight korean language model to address the aforementioned shortcomings of existing language models.

## Quick tour
```python
from transformers import AutoTokenizer, AutoModel

tokenizer = AutoTokenizer.from_pretrained("BM-K/KoMiniLM") # 23M model
model = AutoModel.from_pretrained("BM-K/KoMiniLM")

inputs = tokenizer("안녕 세상아!", return_tensors="pt")
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
|KoBERT(KLUE)| 110M | 86.84 | 90.20±0.07 | 87.11±0.05 | 81.36±0.21 | 81.06±0.33 | 82.47±0.14 | 95.03±0.44 | 84.43±0.18 / <br>93.05±0.04 |
|KcBERT| 108M | 78.94 | 89.60±0.10 | 84.34±0.13 | 67.02±0.42| 74.17±0.52 | 76.57±0.51 | 93.97±0.27 | 60.87±0.27 / <br>85.01±0.14 |
|KoBERT(SKT)| 92M | 79.73 | 89.28±0.42 | 87.54±0.04 | 80.93±0.91 | 78.18±0.45 | 75.98±2.81 | 94.37±0.31  | 51.94±0.60 / <br>79.69±0.66 |
|DistilKoBERT| 28M | 74.73 | 88.39±0.08 | 84.22±0.01 | 61.74±0.45 | 70.22±0.14 | 72.11±0.27 | 92.65±0.16 | 52.52±0.48 / <br>76.00±0.71 |
|  |  |  |  |  |  |  |  |  |
|**KoMiniLM<sup>†</sup>**| **68M** | 85.90 | 89.84±0.02 | 85.98±0.09 | 80.78±0.30 | 79.28±0.17 | 81.00±0.07 | 94.89±0.37 | 83.27±0.08 / <br>92.08±0.06 |
|**KoMiniLM<sup>†</sup>**| **23M** | 84.79 | 89.67±0.03 | 84.79±0.09 | 78.67±0.45 | 78.10±0.07 | 78.90±0.11 | 94.81±0.12 | 82.11±0.42 / <br>91.21±0.29 |

- [NSMC](https://github.com/e9t/nsmc) (Naver Sentiment Movie Corpus)
- [Naver NER](https://github.com/naver/nlp-challenge) (NER task on Naver NLP Challenge 2018)
- [PAWS](https://github.com/google-research-datasets/paws) (Korean Paraphrase Adversaries from Word Scrambling)
- [KorNLI/KorSTS](https://github.com/kakaobrain/KorNLUDatasets) (Korean Natural Language Understanding)
- [Question Pair](https://github.com/songys/Question_pair) (Paired Question)
- [KorQuAD](https://korquad.github.io/) (The Korean Question Answering Dataset)

<img src = "https://user-images.githubusercontent.com/55969260/174229747-279122dc-9d27-4da9-a6e7-f9f1fe1651f7.png"> <br>

## License
This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br />

## Reference
- [KLUE BERT](https://github.com/KLUE-benchmark/KLUE)
- [KcBERT](https://github.com/Beomi/KcBERT)
- [SKT KoBERT](https://github.com/SKTBrain/KoBERT)
- [DistilKoBERT](https://github.com/monologg/DistilKoBERT)
- [lassl](https://github.com/lassl/lassl)

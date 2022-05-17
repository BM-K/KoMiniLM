# KoMiniLM
💪 Korean light weight language model

## Why
- 서비스 측면에서 큰 용량을 갖는 기존 언어 모델의 한계를 보완하고자 경량화된 언어 모델을 공개합니다.

## Quick tour
`NOTE`: **KoMiniLM** will be released as open source.
```python
from transformers import AutoTokenizer, AutoModel

# KoMiniLM-68M (68M)
tokenizer = AutoTokenizer.from_pretrained("BM-K/")
model = AutoModel.from_pretrained("BM-K/")

# KoMiniLM-23M (23M)
tokenizer = AutoTokenizer.from_pretrained("BM-K/")
model = AutoModel.from_pretrained("BM-K/")

inputs = tokenizer("안녕 세상아!", return_tensors="pt")
outputs = model(**inputs)
```

## Pre-training
`Teacher Model`: [KLUE-BERT(base)](https://github.com/KLUE-benchmark/KLUE)
### Object
- Self-Attention Distribution 및 Self-Attention Value-Relation [[Wang et al., 2020]](https://arxiv.org/abs/2002.10957)을 교사 모델의 불연속적인 각 층에서 학생 모델로 증류하였습니다.
### Data set
|데이터|뉴스댓글|뉴스기사|
|:----:|:----:|:----:|
|크기|10G|10G|
### Config
- **KoMiniLM-68M**
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
- **KoMiniLM-23M**
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
## Performance on subtask
|| #Param | NSMC<br>(Acc) | Naver NER<br>(F1) | PAWS<br>(Acc) | KorNLI<br>(Acc) | KorSTS<br>(Spearman) | Question Pair<br>(Acc) | KorQuaD<br>(Dev)<br>(EM/F1) | 
|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|
|KoBERT(KLUE)| 110M | 90.20±0.07 | 87.11±0.05 | 81.36±0.21 | 81.06±0.33 | 82.47±0.14 | 95.03±0.44 | 84.43±0.18 / <br>93.05±0.04 |
|KcBERT| 108M | 89.60±0.10 | 84.34±0.13 | 67.02±0.42| 74.17±0.52 | 76.57±0.51 | 93.97±0.27 | 60.87±0.27 / <br>85.01±0.14 |
|KoBERT(SKT)| 92M | 89.28±0.42 | 87.54±0.04 | 80.93±0.91 | 78.18±0.45 | 75.98±2.81 | 94.37±0.31  | 51.94±0.60 / <br>79.69±0.66 |
|DistilKoBERT| 28M | 88.39±0.08 | 84.22±0.01 | 61.74±0.45 | 70.22±0.14 | 72.11±0.27 | 92.65±0.16 | 52.52±0.48 / <br>76.00±0.71 |
|  |  |  |  |  |  |  |  |  |
|**KoMiniLM<sup>†</sup>**| **-M** | 89.72 | 85.87 | 80.5 | 79.44 | 80.90 | 94.06 | 82.78 / 91.84|
|**KoMiniLM<sup>v2</sup>**| **23M** | 89.68 | 84.83 | 79.2 | 78.00 | 79.04 | 94.98 | 82.66 / 91.62 |

## ToDo
- [X] An average of 3 runs for each task
- [ ] Training the entire KoMiniLM
- [ ] Huggingface model porting

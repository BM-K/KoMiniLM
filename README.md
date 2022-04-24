# KoLBERT
Korean Light weight BERT 🍔❌

# Usage
**KoLBERT** will be released as open source.

# Performance
|| #Param | NSMC<br>(Acc) | Naver NER<br>(F1) | PAWS<br>(Acc) | KorNLI<br>(Acc) | KorSTS<br>(Spearman) | Question Pair<br>(Acc) | KorQuaD<br>(Dev)<br>(EM/F1) | 
|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|
|KoBERT(KLUE)| 110M | 90.1 | 87.09 | 81.15 | 81.47 | 82.42 | 94.45 | 84.22 / 93.03 |
|KoBERT(KLUE)| 110M | 90.25 | 87.18 | 81.65 | 80.67 | 82.33 | 95.12 | 84.67 / 93.11 |
|KcBERT| 108M | 89.46 | 84.24 | 67.45 | 73.45 | 76.51 | 93.66 | 60.72 / 84.97 |
|KcBERT| 108M | 89.68 | 84.25 | 66.45 | 74.41 | 75.98 | 93.93 | 61.25 / 85.19 |
|KoBERT(SKT)| 92M | 88.69 | 87.48 | 80.65 | 78.66 | 79.97 | 93.93 | 52.51 / 80.35 |
|KoBERT(SKT)| 92M | 89.58 | 87.54 | 80.7 | 79.14 | 73.93 | 94.59 | 51.11 / 78.78 |
|DistilKoBERT| 28M | 88.34 | 84.23 | 62.25 | 70.33 | 72.5 | 92.87 | 52.11 / 75.94 |
|DistilKoBERT| 28M | 88.32 | 84.24 | 61.15 | 70.3 | 71.94 | 92.61 | 52.25 / 76.16 |
|  |  |  |  |  |  |  |  |  |
|**KoLBERT**| **23M** | 89.41 | 84.52 | 67.45 | 76.56 | 78.15 | 94.98 | 79.45 / 88.92 |

`KoLBERT`: 저는 아직 제 힘의 절반만 사용했습니다만..?

## ToDo
- [ ] An average of 3 runs for each task
- [ ] Training the entire KoLBERT
- [ ] Huggingface model porting

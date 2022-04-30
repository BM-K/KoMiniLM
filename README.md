# KoLBERT
💪 Korean Light weight BERT

# Usage
**KoLBERT** will be released as open source.

# Performance
|| #Param | NSMC<br>(Acc) | Naver NER<br>(F1) | PAWS<br>(Acc) | KorNLI<br>(Acc) | KorSTS<br>(Spearman) | Question Pair<br>(Acc) | KorQuaD<br>(Dev)<br>(EM/F1) | 
|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|
|KoBERT(KLUE)| 110M | 90.20±0.07 | 87.11±0.05 | 81.36±0.21 | 81.06±0.33 | 82.47±0.14 | 95.03±0.44 | 84.43±0.18 / 93.05±0.04 |
|KcBERT| 108M | 89.60±0.10 | 84.34±0.13 | 67.02±0.42| 74.17±0.52 | 76.57±0.51 | 93.97±0.27 | 60.87±0.27 / 85.01±0.14 |
|KoBERT(SKT)| 92M | 88.69 | 87.48 | 80.65 | 78.66 | 79.97 | 93.93 | 52.51 / 80.35 |
|KoBERT(SKT)| 92M | 89.58 | 87.54 | 80.7 | 79.14 | 73.93 | 94.59 | 51.11 / 78.78 |
|KoBERT(SKT)| 92M | 89.59 | 87.6 | 78.75 | 79.76 |  74.06 | 94.59  | 52.21 / 79.95 |
|KoBERT(SKT)| 92M |  |  |  |  |   |   |  /  |
|DistilKoBERT| 28M | 88.34 | 84.23 | 62.25 | 70.33 | 72.5 | 92.87 | 52.11 / 75.94 |
|DistilKoBERT| 28M | 88.32 | 84.24 | 61.15 | 70.3 | 71.94 | 92.61 | 52.25 / 76.16 |
|DistilKoBERT| 28M | 88.51 | 84.2 | 61.85 | 70.03 | 71.91 | 92.48 | 53.2 / 76.9 |
|DistilKoBERT| 28M |  |  |  |  |  |  |  /  |
|  |  |  |  |  |  |  |  |  |
|**KoLBERT<sup>†</sup>**| **23M** | 89.64 | 84.4 | 75.1 | 77.16 | 78.23 | 94.98 | 81.0 / 90.27 |

## ToDo
- [X] An average of 3 runs for each task
- [ ] Training the entire KoLBERT
- [ ] Huggingface model porting

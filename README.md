# KoLBERT
💪 Korean Light weight BERT

# Usage
**KoLBERT** will be released as open source.

# Performance
|| #Param | NSMC<br>(Acc) | Naver NER<br>(F1) | PAWS<br>(Acc) | KorNLI<br>(Acc) | KorSTS<br>(Spearman) | Question Pair<br>(Acc) | KorQuaD<br>(Dev)<br>(EM/F1) | 
|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|
|KoBERT(KLUE)| 110M | 90.20<br>±0.07 | 87.11<br>±0.05 | 81.36<br>±0.21 | 81.06<br>±0.33 | 82.47<br>±0.14 | 95.03<br>±0.44 | 84.43±0.18/ 93.05±0.04 |
|KcBERT| 108M | 89.60<br>±0.10 | 84.34<br>±0.13 | 67.02<br>±0.42| 74.17<br>±0.52 | 76.57<br>±0.51 | 93.97<br>±0.27 | 60.87±0.27/ 85.01±0.14 |
|KoBERT(SKT)| 92M | 89.28<br>±0.42 | 87.54<br>±0.04 | 80.93<br>±0.91 | 78.18<br>±0.45 | 75.98<br>±2.81 | 94.37<br>±0.31  | 51.94±0.60/ 79.69±0.66 |
|DistilKoBERT| 28M | 88.39<br>±0.08 | 84.22<br>±0.01 | 61.74<br>±0.45 | 70.22<br>±0.14 | 72.11<br>±0.27 | 92.65<br>±0.16 | 52.52±0.48/ 76.00±0.71 |
|  |  |  |  |  |  |  |  |  |
|**KoLBERT<sup>†</sup>**| **23M** | 89.64 | 84.4 | 75.1 | 77.16 | 78.23 | 94.98 | 81.0 / 90.27 |

## ToDo
- [X] An average of 3 runs for each task
- [ ] Training the entire KoLBERT
- [ ] Huggingface model porting

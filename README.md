# KoLBERT
💪 Korean Light weight BERT

# Usage
**KoLBERT** will be released as open source.

# Performance
|| #Param | NSMC<br>(Acc) | Naver NER<br>(F1) | PAWS<br>(Acc) | KorNLI<br>(Acc) | KorSTS<br>(Spearman) | Question Pair<br>(Acc) | KorQuaD<br>(Dev)<br>(EM/F1) | 
|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|
|KoBERT(KLUE)| 110M | 90.20±0.07 | 87.11±0.05 | 81.36±0.21 | 81.06±0.33 | 82.47±0.14 | 95.03±0.44 | 84.43±0.18/ 93.05±0.04 |
|KcBERT| 108M | 89.60±0.10 | 84.34±0.13 | 67.02±0.42| 74.17±0.52 | 76.57±0.51 | 93.97±0.27 | 60.87±0.27/ 85.01±0.14 |
|KoBERT(SKT)| 92M | 89.28±0.42 | 87.54±0.04 | 80.93±0.91 | 78.18±0.45 | 75.98±2.81 | 94.37±0.31  | 51.94±0.60/ 79.69±0.66 |
|DistilKoBERT| 28M | 88.39±0.08 | 84.22±0.01 | 61.74±0.45 | 70.22±0.14 | 72.11±0.27 | 92.65±0.16 | 52.52±0.48/ 76.00±0.71 |
|  |  |  |  |  |  |  |  |  |
|**KoLBERT<sup>†</sup>**| **23M** | 89.64 | 84.4 | 75.1 | 77.16 | 78.23 | 94.98 | 81.0 / 90.27 |

## ToDo
- [X] An average of 3 runs for each task
- [ ] Training the entire KoLBERT
- [ ] Huggingface model porting

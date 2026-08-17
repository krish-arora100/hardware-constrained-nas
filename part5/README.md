# Part 5

PIC chip QAT experiments layering in data augmentation (random rotation/affine), batch normalization, and learning-rate scheduling (cosine annealing, ReduceLROnPlateau) to recover accuracy lost to quantization.

**Notebook:** [Part5_Code.ipynb](Part5_Code.ipynb) ([open in Colab](https://drive.google.com/file/d/1evrDvR0CMEStxVyCc9FzO96zGplb-l7k/view))

## Results

| Step | LR | Train Acc | Val Acc | Test Acc | Notes |
|---|---|---|---|---|---|
| 1 (all sigmoid) | 0.0005 | 82.64 | - | 81.34 | |
| 1 (all ReLU) | 0.0005 | - | - | - | Didn't train |
| PIC QAT Step 5 - RandRotate/RandAffine, normalized batches, cosine LR anneal | 0.1 -> 0.00001 | - | - | 84.31 | |
| PIC QAT Step 5 - RandRotate/RandAffine, normalized batches, ReduceLROnPlateau | 0.01 -> 0.00001 | 76.86 | - | 85.42 | Val split |
| PIC QAT Step 5, Part 8/2 conv layers, 4x augmented training data | 0.01 (start) | 78.04 | 85.88 | 86.86 | Val split |
| PIC QAT Step 5, normalized batches, 4x augmented training data | 0.01 (start) | 92.53 | 93.47 | 91.51 | Val split |
| PIC QAT Step 5, normalized batches, ReduceLROnPlateau, 4x training data | 0.01 (start) | 94.81 | 95.48 | **91.96** | Val split |

Best result in the captured range: **94.81% train / 91.96% test**, from normalized batches + ReduceLROnPlateau + 4x augmented data.

*(Table sourced from the lab's "Part 5 Results" tracking spreadsheet - the full sheet has additional rows beyond what's summarized here; see the sheet for the complete log.)*

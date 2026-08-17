# Part 4

Direct comparison of quantization-aware training (QAT) vs. full-precision ("no QAT") training across four learning-rate configurations.

**Notebook:** [Part4_Code.ipynb](Part4_Code.ipynb) ([open in Colab](https://drive.google.com/file/d/1-2Y4hgbdSQxMa77zlGlaiQtR9LGgKdpX/view))

## Results

| Step | LR | Train Acc (no QAT) | Train Loss (no QAT) | Test Acc (no QAT) | Train Acc (QAT) | Train Loss (QAT) | Test Acc (QAT) |
|---|---|---|---|---|---|---|---|
| 2 | 0.01 | 95.25 | 1.5 | 94.79 | 93.86 | 1.52 | **94.12** |
| 3 | 0.0005 | 92.13 | 1.54 | 92.07 | 91.78 | 1.54 | 91.51 |
| 4 | 0.01 | 89.23 | 1.57 | 90.03 | 92.72 | 1.54 | **92.89** |
| 5 | 0.01 | 87.62 | 1.58 | 77.81 | 87.16 | 1.59 | 87.25 |

Notable: at step 4, the QAT model actually *outperformed* the full-precision model on test accuracy (92.89% vs. 90.03%).

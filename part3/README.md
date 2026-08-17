# Part 3

Part 2's first EIC attempt only reached ~25% accuracy, so this part systematically steps backward to a standard (non-hardware-constrained) architecture and re-introduces the EIC constraints one at a time (variants A-H) to find where accuracy actually drops. Variant F (all-nonnegative weights) breaks training outright when weights are naively clamped to zero each forward pass; the fix - projected gradient descent (PGD), clamping weights *after* the optimizer step instead - recovers accuracy and is used from variant E/F onward.

**Notebook:** [Part3_Code.ipynb](Part3_Code.ipynb) ([open in Colab](https://colab.research.google.com/drive/1oQOYaWOMmUbM-_nz0teWJa8K1HpHYP46))

## Results

| Step | Train Acc (10ep) | Train Loss | LR | Test Acc | Notes |
|---|---|---|---|---|---|
| A1 | 97.68 | 1.49 | 0.001 | - | |
| A2 | 97.77 | 1.48 | 0.001 | - | |
| A3 | 9.74 | 2.36 | - | - | Didn't learn; tried multiple learning rates |
| B | 95.71 | 1.51 | - | - | |
| C (same as B) | - | - | - | - | Already uses a flatten layer in B |
| D | 96.76 | 1.5 | 0.0005 | - | |
| E | 96.14 | 1.5 | 0.001 | - | |
| F | 13.77 | 2.56 | - | - | Didn't learn; tried multiple learning rates |
| E with PGD | 98.07 | 1.49 | 0.0005 | **97.13** | |
| F with PGD | 57.49 | 1.9 | 0.0005 | - | Same architecture as E, but adds the two weight matrices instead of subtracting them (eliminates negative weights entirely) |
| G with PGD | 95.54 | 1.51 | 0.001 | - | |
| H with PGD | 97.82 | 1.49 | 0.0005 | **97.05** | |

Best result: **E with PGD, 97.13% test accuracy**.

# Part 7

3-core binarized-activation architecture: 8-bit quantized linear layers with a unique shared input distribution (256 overlapping inputs, 256 outputs per core), a custom 8-bit quantized output layer, and full QAT (positive and negative weights, no PGD constraint here). Trained on binarized MNIST.

**Notebook:** [Part7_Code.ipynb](Part7_Code.ipynb) ([open in Colab](https://colab.research.google.com/drive/1fFWmSu40JZdCFRKVIHhiV8raeFx43LVO))

## Results

| Step | LR | Train Acc | Val Acc | Test Acc | Notes |
|---|---|---|---|---|---|
| 7a | 0.005 | 88.17 | 86.9 | 81.47 (pre-conversion) / 81.61 (post-conversion) | 3-core architecture, 60k train / 10k val / 10k test |

*(Table sourced from the lab's "Part 7 Results" tracking spreadsheet.)*

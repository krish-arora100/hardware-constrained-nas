# Part 8

Combined PIC + EIC core architecture: PIC front-end (Conv2d with sum-pooling and per-feature-map custom bias, 28x28 MNIST -> 6x13x13 feature maps) feeding into 15 EIC cores (256 inputs, 256 outputs each), with a final linear/softmax output layer. Iterates on bias handling across cores.

**Notebook (final iteration):** [Part8_Code.ipynb](Part8_Code.ipynb) ([open in Colab](https://colab.research.google.com/drive/1i_6HSEUIH-USFg7iG7-FW914ITl41NXA))

## Results

| Step | LR | Train Acc | Val Acc | Test Acc | Notes |
|---|---|---|---|---|---|
| 8a (PIC only, sigmoid) | 0.001 | 96.23 | 96.0 | **96.0** | |
| 8ba (+ 15 EIC cores) | 0.0001 | 75.73 | 78.05 | 77.96 | 83.39% test accuracy achieved with 20 epochs |
| 8bab | 0.0001 | 96.8 | 98.75 | **96.43** | 100 epochs |
| 8ba (correct bias) | 0.0001 | 84.52 | 84.4 | 85.17 | |

Best result: **8bab, 96.43% test accuracy** (100 epochs).

## All notebooks in this part

- [Chip_Part8a_02-14-25](https://colab.research.google.com/drive/1uZJjbHtb8i6zI17yke-XoRapLhT7Ahsr)
- [Chip_Part8ba_02-14-25](https://colab.research.google.com/drive/1jvI2TNPkiFECxMBBnYr4Ol5pCI53yAWn)
- [Chip_Part8bab_02-14-25](https://colab.research.google.com/drive/10Rwa1EARhGK24TNBLXdQFEuu-G2xIh3j)
- [Chip_Part8c_02-15-25](https://colab.research.google.com/drive/1pgaROwHgenI_JZ6kXWBtmBOpoTEZMOqb)
- [Chip_Part8cd_02-15-25](https://colab.research.google.com/drive/1feWPq8GGP8Uyj38NAqJ31cLKTuDhjame)
- [Part8ci_02-23-25 (earlier version, Feb 23)](https://colab.research.google.com/drive/1MkScpkFsHYMolBYa2kFp0nv6H3YRcuD7)
- [Part8ci_02-23-25 (final, Mar 7)](https://colab.research.google.com/drive/1i_6HSEUIH-USFg7iG7-FW914ITl41NXA) (linked above)

# Part 6

Binarized-MNIST experiments on a "Basic Network, No CNN" architecture, iterating through per-core 8-bit weight quantization, quantized bias terms, and single-bias-per-layer variants. This part had the most iteration notebooks (6, 6a, 6b, 6e, 6eb, 6f, 6g, 6h, 6ia-6ii, 6m, 6n, 6sa-6sc) - the final/most-recently-updated one is linked below.

**Notebook (final iteration):** [Part6_Code.ipynb](Part6_Code.ipynb) ([open in Colab](https://colab.research.google.com/drive/1GsR8hn8tw-gWgGMtIB6fWxO-r8jgakKJ))

## Results

| Step | LR | Train Acc | Val Acc | Test Acc | Notes |
|---|---|---|---|---|---|
| 6a | 0.001 | 99.42 | 99.04 | **97.54** | Basic Network No CNN, 128 batch, binarized MNIST |
| 6 (+ 1-bit activation QAT) | 0.001 | 99.43 | 98.99 | 97.55 | |
| 6b (8-bit weights QAT, quant stubs) | 0.001 | 99.38 | 99.18 | 97.66 | |
| 6e (+ single bias term) | 0.001 | 99.49 | 99.19 | **97.78** | |
| 6f (+ single bias term per layer) | 0.001 | 99.4 | 99.09 | 97.5 | |
| 6eb (+ 8-bit bias, manual, single bias per layer) | 0.001 | 99.35 | 99.01 | 97.3 | |

Best result: **6e, 97.78% test accuracy**.

## All notebooks in this part

Part 6 had the most iteration notebooks of any part. In rough chronological order:

- [Chip_Part6_01-26-25](https://colab.research.google.com/drive/1Q56Bm2glxKU1_fl7uP-_Rgl8aFaV11oe)
- [Chip_Part6a_01-27-25](https://colab.research.google.com/drive/1U_1zF3u9IDhbuCAoK4n331c6wg9R_Yly)
- [Chip_Part6b_02-1-25](https://colab.research.google.com/drive/1e1p-TArsLt0Xhw9Doo9shiM2CE_itr07)
- [Chip_Part6e_02-1-25](https://colab.research.google.com/drive/1Gp8tCkUinGaHrQdMZ2sekBNfj9KEg9Oa)
- [Chip_Part6eb_02-8-25](https://colab.research.google.com/drive/1CG02Df-aFYNNGgoK8SsHj81dwVi8KcWe)
- [Chip_Part6f_02-1-25](https://colab.research.google.com/drive/19mCY5haDUOqcj0RHI-zwMrRSBymbTj-p)
- [Chip_Part6g_02-8-25](https://colab.research.google.com/drive/11UNIuFmrbGp-YSOX-JuCA79b2FJ4ZF3E)
- [Chip_Part6h_02-10-25](https://colab.research.google.com/drive/12rXT-Sub9VBSYeqsHftHABhyxAA0IQfY)
- [Chip_Part6ia_02-8-25](https://colab.research.google.com/drive/1073mSdROzLfEFEghih0-7PoAU-wC1R6m)
- [Chip_Part6id_02-10-25](https://colab.research.google.com/drive/1AJriLEZUl3RA6eddf4gYhNcyQEbwzIjo)
- [Chip_Part6ie_02-11-25](https://colab.research.google.com/drive/1tLkKSgQRtMTOyqcWmYtCiwiihtCce-NB)
- [Chip_Part6ih_02-11-25](https://colab.research.google.com/drive/1n-ddpYNbnF1H11ZG5xmZBTQyCtWA9ssY)
- [Chip_Part6ii_02-11-25](https://colab.research.google.com/drive/1t8yshiwYVGzKqiEYnvt5FembEPK4HYbN)
- [Chip_Part6m_02-11-25](https://colab.research.google.com/drive/1IcIQrOdPIr4GtN2jZMdvj95C29OqL6QV)
- [Chip_Part6n_02-11-25](https://colab.research.google.com/drive/1h9JoQJM2OGrpKbLRSQUYZrFSg_pYmn-6)
- [Chip_Part6sa_02-12-25](https://colab.research.google.com/drive/1GsR8hn8tw-gWgGMtIB6fWxO-r8jgakKJ) (final, linked above)
- [Chip_Part6sb_02-12-25](https://colab.research.google.com/drive/141RepsrXMItd4uRXV7gXPE-sDg8vUWLY)
- [Chip_Part6sc_02-12-25](https://colab.research.google.com/drive/1hqVN0mQkM9CjvxmKXMjEr-I6I2gfiH2Q)

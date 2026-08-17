# Part 2

The first full PIC + EIC architecture attempt, at full 32-bit precision (no quantization yet). No results-tracking spreadsheet exists for this part (tracking started at Part 3).

**What it does:** Takes the Part 1 conv layer, average-pools the six 14x14 feature maps down to six 7x7 maps (294 activations), and feeds two overlapping 256-element slices of that vector into two EIC "core" sublayers (each splitting its input into two 128-element halves, multiplying by separate learnable weight matrices, subtracting the results - the trick used to emulate signed weights on RRAM hardware that can only store nonnegative values). The two sublayer outputs feed a final 10-way softmax output layer. This first attempt only reached ~25% accuracy, which motivated the systematic architecture sweep in Part 3.

**Notebook:** [Part2_Code.ipynb](Part2_Code.ipynb) ([open in Colab](https://colab.research.google.com/drive/169WG1HrjeFWhtmqDf-gqFkK2biXSHj1Z))

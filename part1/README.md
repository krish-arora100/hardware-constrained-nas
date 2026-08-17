# Part 1

The first coding step of the project: purely the "PIC" side of the chip, before any EIC constraints are introduced. No results-tracking spreadsheet exists for this part (tracking started at Part 3).

**What it does:** Loads MNIST, downsamples the images to 14x14, and implements a convolutional layer with 4-bit weights, 6 kernels (3x3, stride 1, zero padding), and ReLU activations - producing six 14x14 feature maps. This models what the PIC (photonic) side of the chip will compute; the EIC (electronic) side isn't modeled yet.

**Notebook:** [Part1_Code.ipynb](Part1_Code.ipynb) ([open in Colab](https://drive.google.com/file/d/1-4mJUmxQnaK5Qp2PlJ-1pfMBZxIjGLSl/view))

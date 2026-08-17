# Hardware-Constrained Neural Architecture Search (EIC / PIC Chip Exploration)

Neural architecture search and quantization-aware training experiments run to fit MNIST classifiers onto a hardware-constrained neuromorphic chip — completed as part of a research internship at UCSD under **Prof. Gert Cauwenberghs** (Cauwenberghs Neuromorphic Systems Lab), advised day-to-day by **Leif Gibb**.

## What this project is

The lab is part of a multi-institution, multi-company effort to build an **EPIC (electronic-photonic integrated circuit)**: a chip that combines a **PIC (photonic integrated circuit)**, designed by a team at UC Davis and implementing the network layer(s) closest to the input, with a **EIC (electronic integrated circuit)**, designed by our team at UCSD and implementing the layers farther from the input. The EIC uses RRAM (resistive RAM) to physically represent the neural network's weights, aiming for very high energy efficiency and design simplicity.

Those hardware choices impose hard constraints that a standard CNN doesn't respect:
- **RRAM can only represent nonnegative weights.** To emulate signed weights, inputs are split and run through separate nonnegative and nonpositive weight matrices, whose outputs are then summed/subtracted.
- **Fixed core geometry.** The EIC is a 16x16 array of 256 cores, each implementing up to 256 units with a 256x256 weight matrix (crossbar array). A fully-connected layer bigger than 256 units has to be split across multiple cores.
- **Constrained, "sloted" connectivity.** Each core's inputs/outputs are grouped into 16 slots of 16 connections each, and every input slot can only be wired to a single output slot elsewhere on the chip - this limits which units can talk to each other.
- **No native bias term** on EIC cores.
- **Quantization down to the hardware's actual bit-widths** (down to binarized activations/weights in later parts), needed for the design to be realistic and energy-efficient.

Each "Part" in this repo is a stage of iterating the network architecture and training procedure to close the gap between a full-precision baseline and a design that will actually run on the constrained hardware - the lab's target was 98% test accuracy on MNIST even under these constraints.

Common techniques explored across parts:
- Quantization-aware training (QAT), including per-core 8-bit weight/bias quantization
- Binarized activations and binarized-weight training
- PGD (projected gradient descent) - used as a constrained-weight training step to keep weights nonnegative without breaking gradient-based learning (a torch.clamp-based approach broke training instead)
- Custom "core" architectures matching the chip's fixed fan-in/fan-out per compute unit, including the nonnegative/nonpositive weight-matrix-pair trick above
- Data augmentation (random rotation/affine), LR scheduling (cosine annealing, ReduceLROnPlateau), and early stopping to recover accuracy lost to quantization

## Repo structure

Each `partN/` folder covers one stage of the exploration:

| Part | Focus (see part README for details) |
|---|---|
| [Part 1](part1/README.md) | First coding step: a 4-bit-quantized convolutional layer on downsampled MNIST - the PIC's job, with no EIC constraints yet |
| [Part 2](part2/README.md) | First full PIC + EIC architecture attempt (conv layer + two EIC "core" sublayers + output layer), full 32-bit precision |
| [Part 3](part3/README.md) | Systematic architecture sweep (variants A-H) to find why accuracy dropped when adding nonnegative-weight EIC cores, ending with PGD-based training |
| [Part 4](part4/README.md) | Quantization-aware training vs. full-precision comparison |
| [Part 5](part5/README.md) | PIC QAT with data augmentation and LR scheduling, working toward the 98% accuracy target under quantization |
| [Part 6](part6/README.md) | Binarized MNIST, per-core 8-bit quantization iterations |
| [Part 7](part7/README.md) | 3-core binarized-activation architecture with custom output layer |
| [Part 8](part8/README.md) | PIC + EIC combined core architecture |
| [Part 9](part9/README.md) | Multi-layer core network, cosine LR annealing |

Each part's README has the code and a results table: architecture, learning rate, train/val/test accuracy and loss, and notes. Parts 6, 8, and 9 went through a lot of minor iterations along the way (e.g. `Chip_Part6ia`, `6id`, `6ie`...) - the notebook checked in is the final/most complete one, with the rest linked at the bottom of that part's README.

## Tech stack

PyTorch, Google Colab, quantization-aware training (QAT) tooling, MNIST.

## Status

This ran from December 2024 through March 2025 and reached ~97-98% test accuracy on MNIST under the EIC/PIC hardware constraints by Part 9. In summer 2025, the lab shifted its full focus to **HiAER-Spike**, a much larger and less constrained neuromorphic "supercomputer" system under development at the San Diego Supercomputer Center ([arXiv:2504.03671](https://arxiv.org/pdf/2504.03671)).

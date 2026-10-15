# Conditional Convolutional VAE for MNIST

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)

A label-conditioned generative model that reconstructs MNIST digits and samples images associated with a requested class label from 0 through 9.

## What is implemented

The convolutional encoder combines image features with a one-hot class label before estimating latent mean/log-variance. The decoder receives both the latent vector and class label, making generation conditional on the digit class.

## Configuration and implementation details

| Area | Implementation in the checked-in source |
|---|---|
| **Dataset** | MNIST via `torchvision`; downloaded automatically to `./data` if needed. |
| **Latent size** | 16 dimensions; 10 class labels. |
| **Architecture** | Convolutional encoder and transposed-convolution decoder with one-hot class conditioning. |
| **Objective** | Binary cross-entropy reconstruction term plus beta-weighted KL divergence. |
| **KL schedule** | Warm-up over the first 10 epochs. |
| **Optimizer** | Adam; learning rate `1e-3`. |
| **Training** | 15 epochs; batch size 128. |
| **Device** | CUDA when available, otherwise CPU. |

## Workflow

1. Load MNIST images and integer class labels.
2. Encode image features together with the class label.
3. Train the conditional VAE with reconstruction loss and KL regularization.
4. Display test-image reconstructions with their labels.
5. Draw Gaussian latent samples separately for each class and display the generated grid.

## Run locally

From the repository root:

```bash
cd "cvae-mnist"
python -m venv .venv
# Activate .venv for your shell before continuing.
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
python "cvaeimagemodel.py"
```

The source selects CUDA when available and otherwise runs on CPU. MNIST-based scripts download data through `torchvision` into `./data` if it is not already cached. Text scripts use the small corpus defined in the source. The file has notebook-export origins, so execution is performed as a top-to-bottom script rather than through a dedicated package API.

## Outputs and included evidence

The script displays reconstruction and class-conditional sample grids. The checked-in `output.png` and `labels created.png` files are reference images; the current code uses Matplotlib display calls rather than saving those exact paths.

### Existing repository artifacts

- [`output.png`](./output.png) — Committed reconstruction comparison.
- [`labels created.png`](./labels%20created.png) — Committed class-conditional sample grid.

These are committed reference artifacts. Their presence does not mean that the current script reproduces them byte-for-byte on every environment.

## Limitations and reproducibility

- No quantitative fidelity or class-consistency evaluation is performed for generated samples.
- No model checkpoint is exported for later inference.
- The test loader is configured with shuffling; therefore, the displayed reconstruction examples can vary between runs.

## Intended use

Use this project to inspect a compact implementation of the method, reproduce an educational run, and compare the concept with the other models in the repository. It is not a production inference package or a benchmark claim.

## Source and dependency files

- Entry point: [`cvaeimagemodel.py`](./cvaeimagemodel.py)
- Dependencies: [`requirements.txt`](./requirements.txt)
- Repository index: [root README](../README.md)

## Source-review note

Class conditioning is explicit in the architecture. This is not a digit classifier and should not be evaluated as one.

## Author

**Shubham Kumar Singh**

---

## License

This project is licensed under the MIT License. See the complete [project-local license](./LICENSE).

```text
MIT License

Copyright (c) 2026 Shubham Kumar Singh

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

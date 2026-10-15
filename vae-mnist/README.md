# Convolutional Variational Autoencoder for MNIST

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)

A convolutional VAE demonstration that reconstructs handwritten digits and samples new images by decoding points drawn from a Gaussian latent prior.

## What is implemented

Two convolutional encoder stages reduce 28 × 28 images to compact feature maps. Separate fully connected heads estimate latent mean and log-variance; reparameterization samples the latent vector; transposed convolutions decode it back to an image.

## Configuration and implementation details

| Area | Implementation in the checked-in source |
|---|---|
| **Dataset** | MNIST via `torchvision`; downloaded automatically to `./data` if missing. |
| **Latent size** | 16 dimensions. |
| **Objective** | Pixel-wise binary cross-entropy reconstruction term plus KL divergence. |
| **KL schedule** | Linear warm-up: `beta = min(1, epoch / 10)`. |
| **Optimizer** | Adam; learning rate `1e-3`. |
| **Training** | 15 epochs; batch size 128. |
| **Device** | CUDA when available, otherwise CPU. |

## Workflow

1. Load and normalize MNIST images.
2. Encode images to latent mean and log-variance values and sample using the reparameterization trick.
3. Optimize reconstruction and KL terms, with KL warm-up.
4. Display eight test images with corresponding reconstructions.
5. Draw random 16-dimensional latent vectors and display decoded samples.

## Run locally

From the repository root:

```bash
cd "vae-mnist"
python -m venv .venv
# Activate .venv for your shell before continuing.
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
python "VAEIMAGE MODEL.py"
```

The source selects CUDA when available and otherwise runs on CPU. MNIST-based scripts download data through `torchvision` into `./data` if it is not already cached. Text scripts use the small corpus defined in the source. The file has notebook-export origins, so execution is performed as a top-to-bottom script rather than through a dedicated package API.

## Outputs and included evidence

The script displays figures with Matplotlib. `output.png` and `random output.png` are committed reference outputs; the current script displays plots rather than writing those exact files with `savefig`.

### Existing repository artifacts

- [`output.png`](./output.png) — Committed reconstruction comparison.
- [`random output.png`](./random%20output.png) — Committed prior-sample grid.

These are committed reference artifacts. Their presence does not mean that the current script reproduces them byte-for-byte on every environment.

## Limitations and reproducibility

- The script reports training loss components but does not compute a standardized held-out image-quality metric.
- No trained weights or inference checkpoint are exported by the script.
- Visual samples vary with initialization, data-loader order, and training environment.

## Intended use

Use this project to inspect a compact implementation of the method, reproduce an educational run, and compare the concept with the other models in the repository. It is not a production inference package or a benchmark claim.

## Source and dependency files

- Entry point: [`VAEIMAGE MODEL.py`](./VAEIMAGE%20MODEL.py)
- Dependencies: [`requirements.txt`](./requirements.txt)
- Repository index: [root README](../README.md)

## Source-review note

This is an unconditional VAE: digit labels are not supplied to the encoder or decoder.

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

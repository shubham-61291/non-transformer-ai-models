# Fully Connected Autoencoder for MNIST

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)

A compact unsupervised image-reconstruction example. An encoder maps each 28 × 28 MNIST image into a 64-dimensional bottleneck; a decoder reconstructs pixels from that representation.

## What is implemented

A fully connected encoder/decoder rather than a convolutional architecture. The input is flattened from 784 pixels, compressed through 256 and 128 units to 64 latent values, and expanded back to a 28 × 28 image with a sigmoid output.

## Configuration and implementation details

| Area | Implementation in the checked-in source |
|---|---|
| **Dataset** | MNIST via `torchvision.datasets.MNIST`; downloaded automatically to `./data` when needed. |
| **Model** | 784 → 256 → 128 → 64 → 128 → 256 → 784; ReLU hidden layers; sigmoid image output. |
| **Objective** | Binary cross-entropy between input and reconstructed pixel values. |
| **Optimizer** | AdamW; learning rate `1e-3`; weight decay `1e-4`. |
| **Training** | 20 epochs; batch size 128. |
| **Device** | CUDA when available, otherwise CPU. |

## Workflow

1. Load MNIST and convert images to tensors in the `[0, 1]` range.
2. Train the autoencoder to reconstruct each input image.
3. Display the training-loss curve.
4. Display eight source images alongside their reconstructions from the test loader.

## Run locally

From the repository root:

```bash
cd "autoencoder-mnist"
python -m venv .venv
# Activate .venv for your shell before continuing.
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
python "AE IMAGE MODEL.py"
```

The source selects CUDA when available and otherwise runs on CPU. MNIST-based scripts download data through `torchvision` into `./data` if it is not already cached. Text scripts use the small corpus defined in the source. The file has notebook-export origins, so execution is performed as a top-to-bottom script rather than through a dedicated package API.

## Outputs and included evidence

The script displays figures with Matplotlib. `output.png` and `training loss curve.png` are reference artifacts already checked into the repository; the current script uses `plt.show()` and does not itself save those exact files.

### Existing repository artifacts

- [`output.png`](./output.png) — Committed reconstruction comparison.
- [`training loss curve.png`](./training%20loss%20curve.png) — Committed training-loss plot.

These are committed reference artifacts. Their presence does not mean that the current script reproduces them byte-for-byte on every environment.

## Limitations and reproducibility

- The evaluation is qualitative: the script does not calculate a held-out reconstruction metric such as test BCE or pixel MSE.
- The code does not save a reusable model checkpoint.
- This is a dense baseline; it does not exploit the local spatial structure of images the way a convolutional autoencoder would.

## Intended use

Use this project to inspect a compact implementation of the method, reproduce an educational run, and compare the concept with the other models in the repository. It is not a production inference package or a benchmark claim.

## Source and dependency files

- Entry point: [`AE IMAGE MODEL.py`](./AE%20IMAGE%20MODEL.py)
- Dependencies: [`requirements.txt`](./requirements.txt)
- Repository index: [root README](../README.md)

## Source-review note

The model uses MNIST labels only as part of the loader tuple; the labels are not passed to the autoencoder or used as supervised targets.

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

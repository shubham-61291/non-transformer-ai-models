# Deep Convolutional GAN for MNIST

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)

A convolutional GAN reference implementation for generating MNIST digits using a transposed-convolution generator and convolutional discriminator.

## What is implemented

The generator projects a 100-dimensional latent vector to a 7 × 7 feature map and upsamples to 28 × 28. The discriminator downsamples images with convolutional layers and predicts a real/fake score.

## Configuration and implementation details

| Area | Implementation in the checked-in source |
|---|---|
| **Dataset** | MNIST via `torchvision`; pixels are normalized to `[-1, 1]`. |
| **Latent input** | 100-dimensional Gaussian noise. |
| **Architecture** | Convolutional discriminator and transposed-convolution generator, with batch normalization in the generator. |
| **Objective** | Binary cross-entropy adversarial objective. |
| **Optimizer** | Adam for generator and discriminator; betas `(0.5, 0.999)`; learning rate `2e-4`. |
| **Training** | 20 epochs; batch size 128. |
| **Monitoring** | Display fixed-noise samples every 5 epochs and generator/discriminator loss plots. |
| **Device** | CUDA when available, otherwise CPU. |

## Workflow

1. Load MNIST images using the `[-1, 1]` scale expected by the generator’s `tanh` output.
2. Initialize convolutional weights using the custom initialization routine.
3. Alternate discriminator and generator updates each batch.
4. Display a 16-image grid at epochs divisible by five.
5. Plot adversarial losses at the end of training.

## Run locally

From the repository root:

```bash
cd "dcgan-mnist"
python -m venv .venv
# Activate .venv for your shell before continuing.
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
python "DCGAN.py"
```

The source selects CUDA when available and otherwise runs on CPU. MNIST-based scripts download data through `torchvision` into `./data` if it is not already cached. Text scripts use the small corpus defined in the source. The file has notebook-export origins, so execution is performed as a top-to-bottom script rather than through a dedicated package API.

## Outputs and included evidence

The script displays figures with Matplotlib. Epoch snapshots and `training loss.png` are committed reference artifacts and are not written to those exact filenames by the current script.

### Existing repository artifacts

- [`after 5 epoch.png`](./after%205%20epoch.png) — Committed sample grid.
- [`after 10 epoch.png`](./after%2010%20epoch.png) — Committed sample grid.
- [`after 15 epoch.png`](./after%2015%20epoch.png) — Committed sample grid.
- [`after 20 epoch.png`](./after%2020%20epoch.png) — Committed sample grid.
- [`training loss.png`](./training%20loss.png) — Committed adversarial-loss plot.

These are committed reference artifacts. Their presence does not mean that the current script reproduces them byte-for-byte on every environment.

## Limitations and reproducibility

- The project does not compute quantitative image-generation quality metrics.
- Adversarial training is sensitive to random initialization and optimization settings.
- No trained checkpoint is exported. GPU use is optional and availability depends on the local PyTorch installation.

## Intended use

Use this project to inspect a compact implementation of the method, reproduce an educational run, and compare the concept with the other models in the repository. It is not a production inference package or a benchmark claim.

## Source and dependency files

- Entry point: [`DCGAN.py`](./DCGAN.py)
- Dependencies: [`requirements.txt`](./requirements.txt)
- Repository index: [root README](../README.md)

## Source-review note

DCGAN uses spatial convolutional layers, unlike the fully connected GAN baseline in `../gan-mnist/README.md`.

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

# Vanilla Generative Adversarial Network for MNIST

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)

A baseline GAN that learns to synthesize 28 × 28 handwritten digit-like images from random latent noise using an adversarial generator/discriminator game.

## What is implemented

Both generator and discriminator are fully connected networks. The generator maps a 100-dimensional random vector through hidden layers to 784 pixels with `tanh`; the discriminator flattens each image and predicts real/fake probability with a sigmoid output.

## Configuration and implementation details

| Area | Implementation in the checked-in source |
|---|---|
| **Dataset** | MNIST via `torchvision`; images are scaled to `[-1, 1]`. |
| **Latent input** | 100-dimensional Gaussian noise. |
| **Networks** | Fully connected generator and discriminator; hidden width parameter 256. |
| **Objective** | Binary cross-entropy adversarial objective. |
| **Optimizer** | Adam for both networks; learning rate `2e-4`; betas `(0.5, 0.999)`. |
| **Training** | 50 epochs; batch size 128. |
| **Monitoring** | Display a fixed-noise sample grid every 10 epochs and generator/discriminator loss curves. |
| **Device** | CUDA when available, otherwise CPU. |

## Workflow

1. Download/load MNIST and scale image values to the generator’s output range.
2. Update the discriminator with real images and generated images.
3. Update the generator to produce images the discriminator classifies as real.
4. Display fixed-noise sample grids every 10 epochs.
5. Plot both adversarial loss traces after training.

## Run locally

From the repository root:

```bash
cd "gan-mnist"
python -m venv .venv
# Activate .venv for your shell before continuing.
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
python "gan model.py"
```

The source selects CUDA when available and otherwise runs on CPU. MNIST-based scripts download data through `torchvision` into `./data` if it is not already cached. Text scripts use the small corpus defined in the source. The file has notebook-export origins, so execution is performed as a top-to-bottom script rather than through a dedicated package API.

## Outputs and included evidence

The script displays sample grids and loss plots. The repository’s epoch snapshots and `Gan training loss.png` are committed reference artifacts; this version uses `plt.show()` rather than saving those named files.

### Existing repository artifacts

- [`after 10 epoch.png`](./after%2010%20epoch.png) — Committed sample grid.
- [`after 20 epoch.png`](./after%2020%20epoch.png) — Committed sample grid.
- [`after 30 epoch.png`](./after%2030%20epoch.png) — Committed sample grid.
- [`after 40 epoch.png`](./after%2040%20epoch.png) — Committed sample grid.
- [`after 50 epoch.png`](./after%2050%20epoch.png) — Committed sample grid.
- [`Gan training loss.png`](./Gan%20training%20loss.png) — Committed adversarial-loss plot.

These are committed reference artifacts. Their presence does not mean that the current script reproduces them byte-for-byte on every environment.

## Limitations and reproducibility

- GAN loss curves do not directly measure image quality or mode coverage.
- No FID, precision/recall for generative models, or other quantitative sample metric is calculated.
- The script does not export model weights. The committed sample images are illustrative results, not a guarantee of identical output on every run.

## Intended use

Use this project to inspect a compact implementation of the method, reproduce an educational run, and compare the concept with the other models in the repository. It is not a production inference package or a benchmark claim.

## Source and dependency files

- Entry point: [`gan model.py`](./gan%20model.py)
- Dependencies: [`requirements.txt`](./requirements.txt)
- Repository index: [root README](../README.md)

## Source-review note

This is a dense, fully connected GAN; the convolutional variant is documented separately in `../dcgan-mnist/README.md`.

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

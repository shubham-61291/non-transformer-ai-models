# Diffusion-Style Image Generation Prototype for MNIST

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)

An educational prototype of a Gaussian forward-noising process and a learned noise-prediction network for MNIST-sized grayscale images.

## What is implemented

A linear beta schedule creates 200 forward diffusion steps. A small stack of convolutional layers predicts noise and the script includes a reverse-update sampling loop initialized with random noise.

## Configuration and implementation details

| Area | Implementation in the checked-in source |
|---|---|
| **Dataset** | MNIST via `torchvision`; image tensors are mapped to `[-1, 1]`. |
| **Noise schedule** | 200 timesteps; beta values linearly increase from `1e-4` to `0.02`. |
| **Denoiser** | Small convolutional stack; it accepts `t` in its method signature but does not use the timestep inside the network. |
| **Objective** | Mean squared error between sampled noise and predicted noise. |
| **Optimizer** | Adam; learning rate defined in script. |
| **Training** | 10 epochs; batch size 128. |
| **Device** | CUDA when available, otherwise CPU. |

## Workflow

1. Load MNIST images in the range used by the noise process.
2. Sample a random timestep per training image and add noise according to the cumulative alpha schedule.
3. Train the convolutional network to predict the injected noise.
4. Display a clean/noisy/one-step-denoised comparison.
5. Initialize a sample batch from Gaussian noise and run the script’s reverse-update loop, displaying intermediate and final grids.

## Run locally

From the repository root:

```bash
cd "diffusion-mnist"
python -m venv .venv
# Activate .venv for your shell before continuing.
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
python "diffusion image model.py"
```

The source selects CUDA when available and otherwise runs on CPU. MNIST-based scripts download data through `torchvision` into `./data` if it is not already cached. Text scripts use the small corpus defined in the source. The file has notebook-export origins, so execution is performed as a top-to-bottom script rather than through a dedicated package API.

## Outputs and included evidence

The script displays loss, noising/denoising, intermediate-sampling, and final-sample figures. The checked-in PNGs are reference artifacts; the current code displays figures rather than saving all of those specific filenames.

### Existing repository artifacts

- [`output.png`](./output.png) — Committed noising/reconstruction visualization.
- [`sample at t = 100.png`](./sample%20at%20t%20=%20100.png) — Committed intermediate-sample reference.
- [`sample at t = 150.png`](./sample%20at%20t%20=%20150.png) — Committed intermediate-sample reference.
- [`sample at t = 200.png`](./sample%20at%20t%20=%20200.png) — Committed intermediate-sample reference.
- [`final sample.png`](./final%20sample.png) — Committed generated-sample reference.
- [`training loss.png`](./training%20loss.png) — Committed training-loss reference.

These are committed reference artifacts. Their presence does not mean that the current script reproduces them byte-for-byte on every environment.

## Limitations and reproducibility

- This is a learning prototype, not a validated diffusion implementation. Although timestep `t` is passed to the denoiser, the model body returns `self.net(x)` and therefore ignores the timestep. This weakens the intended timestep-conditioned noise-prediction design.
- The visualization labeled denoised is a direct subtraction of predicted noise, not a complete reverse trajectory. The sampler uses a simplified reverse update and its generated quality has not been quantitatively assessed.
- No checkpoint, FID, or other image-generation benchmark is produced. Treat displayed samples as demonstrations, not evidence of production-grade generative quality.

## Intended use

Use this project to inspect a compact implementation of the method, reproduce an educational run, and compare the concept with the other models in the repository. It is not a production inference package or a benchmark claim.

## Source and dependency files

- Entry point: [`diffusion image model.py`](./diffusion%20image%20model.py)
- Dependencies: [`requirements.txt`](./requirements.txt)
- Repository index: [root README](../README.md)

## Source-review note

The timestep-conditioning caveat is important: do not describe the current network as a fully timestep-conditioned U-Net or as a rigorously validated DDPM.

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

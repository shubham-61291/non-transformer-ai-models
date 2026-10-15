# Non-Transformer AI Models

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)

A source-reviewed collection of **10 small generative-model experiments** covering image reconstruction, variational latent-variable models, adversarial image generation, and toy-corpus text generation/denoising. The projects are kept in separate folders so each can be installed and run independently.

> **Scope note:** the repository is predominantly non-transformer, but `text-diffusion` uses a Transformer encoder as its denoiser. This exception is documented explicitly rather than describing every folder as transformer-free.

## Project catalogue

| Project | Modality | Core idea | Source entry point |
|---|---|---|---|
| [Autoencoder — MNIST](./autoencoder-mnist/README.md) | Images | Dense encoder/decoder reconstructs 28 × 28 digits through a 64-D bottleneck. | [`AE IMAGE MODEL.py`](./autoencoder-mnist/AE%20IMAGE%20MODEL.py) |
| [VAE — MNIST](./vae-mnist/README.md) | Images | Convolutional VAE with a 16-D latent distribution; reconstructs and samples digits. | [`VAEIMAGE MODEL.py`](./vae-mnist/VAEIMAGE%20MODEL.py) |
| [CVAE — MNIST](./cvae-mnist/README.md) | Images | Conditions VAE reconstruction and generation on digit labels 0–9. | [`cvaeimagemodel.py`](./cvae-mnist/cvaeimagemodel.py) |
| [GAN — MNIST](./gan-mnist/README.md) | Images | Fully connected adversarial generator/discriminator baseline. | [`gan model.py`](./gan-mnist/gan%20model.py) |
| [DCGAN — MNIST](./dcgan-mnist/README.md) | Images | Convolutional GAN for 28 × 28 digit synthesis. | [`DCGAN.py`](./dcgan-mnist/DCGAN.py) |
| [Diffusion-style — MNIST](./diffusion-mnist/README.md) | Images | Gaussian forward noising and a small noise-prediction prototype. | [`diffusion image model.py`](./diffusion-mnist/diffusion%20image%20model.py) |
| [Text Autoencoder](./text-autoencoder/README.md) | Text | LSTM encoder/decoder reconstructs short toy sentences. | [`AETEXTMODEL.py`](./text-autoencoder/AETEXTMODEL.py) |
| [Text VAE](./vae-text/README.md) | Text | LSTM variational model reconstructs and greedily generates toy text. | [`VAETEXTMODEL.py`](./vae-text/VAETEXTMODEL.py) |
| [Conditional Text VAE](./cvae-text/README.md) | Text | LSTM CVAE conditions toy sentence generation on three example labels. | [`cvae text model.py`](./cvae-text/cvae%20text%20model.py) |
| [Text Denoising / Diffusion](./text-diffusion/README.md) | Text | Timestep-conditioned Transformer denoiser fills tokens corrupted by masking. | [`diffusion text model.py`](./text-diffusion/diffusion%20text%20model.py) |

## Getting started

### 1. Clone the repository

```bash
git clone https://github.com/shubham-61291/non-transformer-ai-models.git
cd non-transformer-ai-models
```

### 2. Choose one project

Each project has its own `requirements.txt`. Enter that folder, install its requirements, and run the source file listed in its README. For example:

```bash
cd autoencoder-mnist
python -m venv .venv
# Activate the environment for your shell before continuing.
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
python "AE IMAGE MODEL.py"
```

Use one virtual environment per project, or create a shared environment only after reconciling dependency requirements. Several projects request `torch>=2.2` and `torchvision>=0.17`; use the official PyTorch installation selector if you need a CUDA-specific build. The code selects CUDA when available and falls back to CPU.

### Dataset and runtime expectations

- **Image projects:** MNIST is fetched using `torchvision.datasets.MNIST(download=True)` and stored beneath the project’s working directory in `./data` if it is not already available. The first execution therefore needs network access unless the dataset is cached.
- **Text projects:** small illustrative sentence corpora and their vocabularies are defined in source code; they do not train on an external text benchmark.
- **Execution style:** the Python files are exports from notebook workflows. They run top-to-bottom, print training logs and normally display plots or generated examples with Matplotlib. A graphical display or notebook/interactive environment may be needed to see figures.
- **Artifacts:** checked-in PNGs are reference output images. The current scripts generally call `plt.show()` and do not write each committed image filename again, nor do they export reusable model checkpoints.

## How to interpret the examples

These implementations are for learning and inspection, not production model releases. A falling training loss is not by itself evidence of good generalization or high-quality generation. Most scripts do not include held-out quantitative metrics, automated tests, model checkpointing, or version-pinned complete environments. Text models use toy corpora and closed vocabularies; their generated strings should not be taken as evidence of general language capability.

### Important implementation caveats

- In `diffusion-mnist`, the denoiser accepts a timestep argument but does not use it in its forward pass. The repository contains a reverse-update loop, but the implementation should be treated as an educational prototype, not as a validated DDPM implementation.
- `text-diffusion` uses a Transformer encoder and is therefore an explicit exception to the repository’s non-transformer theme.
- The text autoencoder’s displayed reconstruction uses the source sequence as decoder input (teacher forcing); it is not a free-running generation test from a latent vector alone.
- The text VAE and conditional text VAE use tiny hand-authored corpora; their vocabulary, label semantics, and output quality are not broadly validated.
- Model weights are not exported by the scripts, so a separate inference-only run is not currently provided.

## Repository layout

```text
non-transformer-ai-models/
├── autoencoder-mnist/
├── cvae-mnist/
├── cvae-text/
├── dcgan-mnist/
├── diffusion-mnist/
├── gan-mnist/
├── text-autoencoder/
├── text-diffusion/
├── vae-mnist/
├── vae-text/
├── LICENSE
└── README.md
```

Each project folder contains its entry-point script, requirements manifest and detailed README; image examples are included where applicable. Each folder now also includes a local `LICENSE` so the README’s `./LICENSE` link works when the project folder is viewed or copied independently.

## Author

**Shubham Kumar Singh**

## License

This repository is licensed under the MIT License. See the complete [root license](./LICENSE).

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

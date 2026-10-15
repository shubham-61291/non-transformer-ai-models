# Masked-Token Text Denoising with a Transformer Denoiser

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)

A discrete, diffusion-inspired text-denoising experiment that progressively masks tokens and trains a model to recover the original tokens.

## What is implemented

The script creates a toy corpus of more than 100 simple sentences and builds a word-level vocabulary. A corruption schedule masks tokens with probability proportional to timestep. The denoiser uses token and timestep embeddings with a Transformer encoder and a vocabulary prediction head.

## Configuration and implementation details

| Area | Implementation in the checked-in source |
|---|---|
| **Data** | Toy sentence corpus embedded directly in the script; no external data download. |
| **Corruption schedule** | 10 discrete masking steps; mask probability increases with timestep. |
| **Denoiser** | Transformer encoder; model dimension 256, 8 attention heads, 3 encoder layers, feed-forward dimension 512, dropout 0.1; includes timestep embedding. |
| **Objective** | Cross-entropy token prediction, ignoring padding tokens. |
| **Optimizer** | AdamW; learning rate `1e-3`; weight decay `1e-4`. |
| **Training** | 50 epochs; batch size 32. |
| **Device** | CUDA when available, otherwise CPU. |

## Workflow

1. Build a word vocabulary from the embedded toy corpus.
2. Sample a timestep and randomly replace eligible input tokens with MASK tokens.
3. Train the Transformer denoiser to predict the clean token sequence.
4. Display the cross-entropy loss curve.
5. Corrupt a sample sentence and iteratively fill masked positions from predicted tokens.

## Run locally

From the repository root:

```bash
cd "text-diffusion"
python -m venv .venv
# Activate .venv for your shell before continuing.
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
python "diffusion text model.py"
```

The source selects CUDA when available and otherwise runs on CPU. MNIST-based scripts download data through `torchvision` into `./data` if it is not already cached. Text scripts use the small corpus defined in the source. The file has notebook-export origins, so execution is performed as a top-to-bottom script rather than through a dedicated package API.

## Outputs and included evidence

The training-loss plot and sample text (clean, corrupted, reconstructed) are displayed. `train ce loss.png` is a committed reference plot; the current script uses `plt.show()` and does not save it to that path.

### Existing repository artifacts

- [`train ce loss.png`](./train%20ce%20loss.png) — Committed training-loss reference.

These are committed reference artifacts. Their presence does not mean that the current script reproduces them byte-for-byte on every environment.

## Limitations and reproducibility

- Important scope exception: despite the repository name, this project uses a Transformer encoder. It should be described as a Transformer-based text-diffusion prototype, not a non-transformer architecture.
- The data are toy sentences with a vocabulary built from the same small corpus; this does not establish linguistic generalization.
- The iterative procedure greedily fills masked positions and is a simple denoising demonstration, not a validated discrete-diffusion benchmark.
- No checkpoint or quantitative text quality metric is exported.

## Intended use

Use this project to inspect a compact implementation of the method, reproduce an educational run, and compare the concept with the other models in the repository. It is not a production inference package or a benchmark claim.

## Source and dependency files

- Entry point: [`diffusion text model.py`](./diffusion%20text%20model.py)
- Dependencies: [`requirements.txt`](./requirements.txt)
- Repository index: [root README](../README.md)

## Source-review note

Keep this exception visible in repository-level documentation rather than claiming that every model in the repository is transformer-free.

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

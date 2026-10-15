# LSTM Variational Autoencoder for Toy Text

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)

A word-level LSTM VAE that learns a latent distribution over short, manually supplied sentences, reconstructs examples, and greedily decodes samples from a Gaussian latent prior.

## What is implemented

The script builds a vocabulary from a toy corpus, encodes sentences with BOS/EOS and padding tokens, uses an embedding plus LSTM encoder to estimate latent mean and log-variance, and decodes through an LSTM initialized from the sampled latent vector.

## Configuration and implementation details

| Area | Implementation in the checked-in source |
|---|---|
| **Data** | Small toy corpus embedded in the Python file; no external dataset is loaded. |
| **Vocabulary** | Word-level vocabulary with PAD, BOS, EOS, and UNK special tokens. |
| **Architecture** | Embedding 64, LSTM hidden size 128, latent size 16. |
| **Objective** | Token cross-entropy reconstruction term plus beta-weighted KL divergence. |
| **KL schedule** | Linear warm-up over the first 15 epochs. |
| **Optimizer** | Adam; learning rate `1e-3`. |
| **Training** | 150 epochs; batch size 4. |
| **Device** | CUDA when available, otherwise CPU. |

## Workflow

1. Build the corpus, vocabulary, and encoded sequences.
2. Train the LSTM VAE with token reconstruction and KL regularization.
3. Print reconstructions for a batch of examples.
4. Draw random latent vectors and use greedy decoding to print five generated strings.

## Run locally

From the repository root:

```bash
cd "vae-text"
python -m venv .venv
# Activate .venv for your shell before continuing.
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
python "VAETEXTMODEL.py"
```

The source selects CUDA when available and otherwise runs on CPU. MNIST-based scripts download data through `torchvision` into `./data` if it is not already cached. Text scripts use the small corpus defined in the source. The file has notebook-export origins, so execution is performed as a top-to-bottom script rather than through a dedicated package API.

## Outputs and included evidence

The script prints training logs, reconstruction examples and five random text generations. No model checkpoint or visual output is saved by the current script.

## Limitations and reproducibility

- A tiny toy corpus and closed vocabulary do not support broad language generation or reliable semantic control.
- Greedy decoding can produce repetitive or low-diversity text; no automated fluency, diversity, or semantic evaluation is included.
- The source trains and generates in one run; there is no standalone inference command that loads a saved checkpoint and matching vocabulary.

## Intended use

Use this project to inspect a compact implementation of the method, reproduce an educational run, and compare the concept with the other models in the repository. It is not a production inference package or a benchmark claim.

## Source and dependency files

- Entry point: [`VAETEXTMODEL.py`](./VAETEXTMODEL.py)
- Dependencies: [`requirements.txt`](./requirements.txt)
- Repository index: [root README](../README.md)

## Source-review note

Treat generated strings as exploratory examples of latent-variable modeling, not as evidence of a capable general-purpose text generator.

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

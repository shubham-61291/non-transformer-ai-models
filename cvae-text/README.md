# Conditional Variational Autoencoder for Toy Text

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)

A small conditional text-generation experiment. An LSTM encoder/decoder VAE conditions its latent representation and decoder on a manually authored category label.

## What is implemented

The script defines a tiny corpus in source code, builds a word-level vocabulary with PAD/BOS/EOS/UNK tokens, embeds tokens and labels, encodes sequences with an LSTM, samples a latent vector, then decodes using an LSTM. Labels are represented as neutral (0), positive (1), and negative (2) in the sample corpus.

## Configuration and implementation details

| Area | Implementation in the checked-in source |
|---|---|
| **Data** | Small hand-authored toy sentence corpus embedded directly in the script; no download is required. |
| **Tokenizer** | Whitespace/regular-expression word tokenization; vocabulary constructed from the toy corpus. |
| **Architecture** | Embedding dimension 64, LSTM hidden size 128, latent size 16; label embeddings are concatenated with latent features. |
| **Objective** | Token cross-entropy with padding ignored plus beta-weighted KL divergence. |
| **KL schedule** | Beta warms from 0.1 toward 1 across the first 10 epochs. |
| **Optimizer** | Adam; learning rate `1e-3`. |
| **Training** | 50 epochs; batch size 2. |
| **Device** | CUDA when available, otherwise CPU. |

## Workflow

1. Build the toy corpus, vocabulary, special-token IDs, and label IDs.
2. Pad/encode sentences into token sequences.
3. Train the conditional VAE using teacher-forced next-token reconstruction and KL regularization.
4. Print a batch of reconstructions with their labels.
5. Sample a Gaussian latent vector for each of the three classes and greedily decode a short sequence.

## Run locally

From the repository root:

```bash
cd "cvae-text"
python -m venv .venv
# Activate .venv for your shell before continuing.
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
python "cvae text model.py"
```

The source selects CUDA when available and otherwise runs on CPU. MNIST-based scripts download data through `torchvision` into `./data` if it is not already cached. Text scripts use the small corpus defined in the source. The file has notebook-export origins, so execution is performed as a top-to-bottom script rather than through a dedicated package API.

## Outputs and included evidence

Training logs, example reconstructions, and label-conditioned generated strings are printed to the console. There are no committed image outputs in this folder.

## Limitations and reproducibility

- The corpus is tiny and hand-authored; the model is an architecture demonstration, not a sentiment classifier or a usable sentiment-conditioned generator.
- The vocabulary is limited to words in the included corpus, so out-of-vocabulary generalization is not supported beyond the UNK token.
- The README’s historical sample logs show KL values becoming close to zero; this can indicate posterior collapse. No held-out text-generation benchmark is run.
- The script does not save a model or vocabulary artifact for independent inference.

## Intended use

Use this project to inspect a compact implementation of the method, reproduce an educational run, and compare the concept with the other models in the repository. It is not a production inference package or a benchmark claim.

## Source and dependency files

- Entry point: [`cvae text model.py`](./cvae%20text%20model.py)
- Dependencies: [`requirements.txt`](./requirements.txt)
- Repository index: [root README](../README.md)

## Source-review note

The label values are conditioning codes attached to the toy data, not labels learned or validated on a real sentiment dataset.

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

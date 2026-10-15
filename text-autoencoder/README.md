# LSTM Text Autoencoder on a Toy Corpus

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)

A compact sequence-to-sequence example that maps short sentences through a low-dimensional latent representation and predicts token sequences for reconstruction.

## What is implemented

A vocabulary is built from ten hand-authored sentences plus special tokens. An embedding layer feeds an LSTM encoder; its final hidden state is projected to a 32-dimensional latent vector, then projected back to the decoder hidden state for an LSTM decoder.

## Configuration and implementation details

| Area | Implementation in the checked-in source |
|---|---|
| **Data** | Ten sample sentences embedded in the script; no external corpus is fetched. |
| **Vocabulary** | Word-level vocabulary with PAD, BOS, EOS, and UNK tokens. |
| **Architecture** | Embedding 64, LSTM hidden size 128, latent size 32. |
| **Objective** | Cross-entropy over vocabulary tokens, ignoring PAD. |
| **Optimizer** | AdamW; learning rate `1e-3`. |
| **Training** | 30 epochs; batch size 2. |
| **Device** | CUDA when available, otherwise CPU. |

## Workflow

1. Create the toy sentence list and word vocabulary.
2. Encode and pad sentences to a fixed sequence length.
3. Train the encoder/decoder network using cross-entropy reconstruction loss.
4. Print one reconstruction example after training.

## Run locally

From the repository root:

```bash
cd "text-autoencoder"
python -m venv .venv
# Activate .venv for your shell before continuing.
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
python "AETEXTMODEL.py"
```

The source selects CUDA when available and otherwise runs on CPU. MNIST-based scripts download data through `torchvision` into `./data` if it is not already cached. Text scripts use the small corpus defined in the source. The file has notebook-export origins, so execution is performed as a top-to-bottom script rather than through a dedicated package API.

## Outputs and included evidence

Loss logs and a text reconstruction example are printed to the console. No figure or model checkpoint is written by the current script.

## Limitations and reproducibility

- The training set contains only ten short sentences, so the model can memorize examples and does not demonstrate general-purpose language understanding.
- The reconstruction helper feeds the encoded input sequence into the decoder while conditioning on the latent state; this is teacher-forced reconstruction rather than free-running text generation from the latent vector alone.
- The displayed sequence may include special tokens such as EOS; the existing README’s example includes repeated end-of-sequence tokens.
- No held-out split, automatic text metric, or checkpoint persistence is implemented.

## Intended use

Use this project to inspect a compact implementation of the method, reproduce an educational run, and compare the concept with the other models in the repository. It is not a production inference package or a benchmark claim.

## Source and dependency files

- Entry point: [`AETEXTMODEL.py`](./AETEXTMODEL.py)
- Dependencies: [`requirements.txt`](./requirements.txt)
- Repository index: [root README](../README.md)

## Source-review note

This is an educational sequence autoencoder, not a transformer language model, retrieval model, or production text compressor.

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

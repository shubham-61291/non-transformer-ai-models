Variational Autoencoder (Text) 📖 Overview

The Variational Autoencoder (Text VAE) is a generative model built using PyTorch. It learns latent representations of text sequences and can both reconstruct input sentences and generate new sentences from the latent space.

🚀 Key Features

✅ Variational Autoencoder with KL annealing.
✅ Learns latent space of short text sentences.
✅ Supports teacher forcing for training.
✅ Can reconstruct input sequences.
✅ Can generate new random sentences from latent space.

🛠 Tech Stack

Framework: PyTorch
Dataset: Custom toy corpus (handcrafted sentences)
Libraries: Torch
Optimizer: AdamW
Loss: Cross-Entropy + KL Divergence

📂 Project Structure

vae-text/
│── VAETEXTMODEL.py # Core training + reconstruction + generation script
│── requirements.txt # Dependencies
│── README.md # Documentation

⚡ Installation

git clone https://github.com/shubham-61291/non-transformer-ai-models.git

cd "vae-text"
pip install -r requirements.txt

▶️ Usage

python "VAETEXTMODEL.py"

This will train the Text VAE, print reconstruction results, and generate random text samples.

🖼 Demo (Text Output)

🔹 Training Logs (sample)
Epoch 01/150 | beta=0.07 | Loss 3.983 Rec 3.983 KL 0.002
Epoch 10/150 | beta=0.67 | Loss 3.061 Rec 3.057 KL 0.005
Epoch 50/150 | beta=1.00 | Loss 0.631 Rec 0.631 KL 0.001
Epoch 100/150 | beta=1.00 | Loss 0.561 Rec 0.548 KL 0.012
Epoch 150/150 | beta=1.00 | Loss 0.555 Rec 0.512 KL 0.042

🔹 Reconstructions
Input: regularization prevents overfitting
Reconstruct: vae prevents overfitting

Input: adamw works well in practice
Reconstruct: i works well in practice

Input: variational autoencoders generate data
Reconstruct: vae autoencoders generate data

Input: latent representations capture meaning
Reconstruct: latent representations capture meaning

🔹 Random Generations
Generated: i love deep learning
Generated: vae is probabilistic
Generated: vae is probabilistic
Generated: vae is probabilistic
Generated: i like machine learning

🔮 Future Enhancements

🔹 Extend to larger text datasets.
🔹 Add Conditional VAE (CVAE) for label-guided generation.
🔹 Use transformer-based encoder/decoder.
🔹 Add perplexity-based evaluation metrics.

👨‍💻 Author

Shubham Singh

📜 License

MIT License

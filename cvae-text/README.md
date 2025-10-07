Conditional Variational Autoencoder for Text (CVAE-Text) 📖 Overview

The Conditional Variational Autoencoder for Text (CVAE-Text) is an extension of the Variational Autoencoder that conditions both the encoder and decoder on class labels. This allows the model to generate text conditioned on sentiment labels (e.g., positive, negative, neutral).

🚀 Key Features

✅ Conditional text generation based on sentiment labels (0 = neutral, 1 = positive, 2 = negative)
✅ Sequence-to-sequence architecture with embeddings and LSTMs
✅ β-VAE training schedule with KL annealing
✅ Reconstruction of input sentences with labels
✅ Random text generation conditioned on labels

🛠 Tech Stack

Framework: PyTorch
Libraries: Torch
Optimizer: Adam
Loss: Cross-Entropy + KL Divergence

📂 Project Structure

cvae-text/
│── cvae text model.py # Core CVAE for text implementation and training
│── requirements.txt # Dependencies
│── README.md # Documentation
│── .gitkeep # To track empty folder in git

⚡ Installation

git clone https://github.com/shubham-61291/non-transformer-ai-models.git

cd "cvae-text"
pip install -r requirements.txt

▶️ Usage

python "cvae text model.py"

This will train the CVAE on the toy corpus and print training logs, reconstructions, and random generations.

🖼 Demo (Text Output)
🔹 Training Logs

Epoch 01/50 | beta=0.10 | Loss 3.358 Rec 3.349 KL 0.086
Epoch 10/50 | beta=1.00 | Loss 2.034 Rec 2.034 KL 0.001
Epoch 20/50 | beta=1.00 | Loss 0.650 Rec 0.649 KL 0.000
Epoch 50/50 | beta=1.00 | Loss 0.257 Rec 0.257 KL 0.000

🔹 Reconstructions with Labels
Label 0 | Input: i love deep learning
Label 0 | Reconstruct:i love deep learning

Label 2 | Input: that film was terrible
Label 2 | Reconstruct:a film was terrible

🔹 Random Generations (Conditioned on Label)

Label 0: i love deep learning
Label 1: an excellent performance
Label 2: a very bad script

🔮 Future Enhancements

🔹 Extend dataset beyond toy corpus
🔹 Add attention mechanism for better text generation
🔹 Evaluate on larger benchmarks like IMDB reviews

👨‍💻 Author

Shubham Singh

📜 License

MIT License

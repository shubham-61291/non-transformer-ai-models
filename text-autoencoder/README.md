# Text Autoencoder 📖 Overview
The Text Autoencoder is a sequence-to-sequence model built using PyTorch that learns to compress and reconstruct sentences. It demonstrates unsupervised learning on small text data by encoding sentences into a latent space and then reconstructing them back.

## 🚀 Key Features
✅ Sequence-to-sequence autoencoder with embeddings and LSTMs.  
✅ Learns latent vector representations of text.  
✅ Reconstruction of input sentences from latent space.  
✅ Trains on a toy dataset of 10 sample sentences.  
✅ Lightweight PyTorch pipeline.  

## 🛠 Tech Stack
Framework: PyTorch  
Libraries: Torch, NumPy  
Model: LSTM Encoder–Decoder Autoencoder  
Optimizer: AdamW  
Loss: CrossEntropyLoss (ignores padding tokens)  

## 📂 Project Structure
text-autoencoder/  
│── AETEXTMODEL.py         # Core training + reconstruction script  
│── requirements.txt       # Dependencies  
│── README.md              # Documentation  

## ⚡ Installation
git clone https://github.com/shubham-61291/non-transformer-ai-models.git  
cd "text-autoencoder"  
pip install -r requirements.txt  

## ▶️ Usage
python "AETEXTMODEL.py"  

This will train the autoencoder for 30 epochs and print vocabulary, loss values, and reconstruction results.

## 🖼 Demo (Text Output)
🔹 **Training Logs (sample)**  
Epoch [1/30], Loss: 3.6090  
Epoch [10/30], Loss: 1.6814  
Epoch [20/30], Loss: 0.3209  
Epoch [30/30], Loss: 0.0936  

🔹 **Reconstruction Example**  
Original: i love deep learning  
Reconstructed: <bos> i love deep learning <eos> <eos> <eos> <eos> <eos> <eos> <eos>  

## 🔮 Future Enhancements
🔹 Add attention mechanism in the decoder.  
🔹 Train on larger text datasets (IMDB, Wikipedia).  
🔹 Extend to Variational Autoencoder (VAE) for text.  
🔹 Build interactive interface for input-output text reconstruction.  

## 👨‍💻 Author
Shubham Singh 

## 📜 License
MIT License

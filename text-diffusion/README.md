Text Diffusion Model 📖 Overview

The Text Diffusion Model applies diffusion-style denoising to text sequences using a Transformer-based denoiser. It reconstructs masked or corrupted tokens through iterative denoising and shows how diffusion concepts extend from images to discrete text data.

🚀 Key Features

✅ Transformer-based denoiser for text sequences
✅ Diffusion-style training with masking noise
✅ Training loss visualization (image)
✅ Text reconstruction outputs (plain text)
✅ Lightweight PyTorch implementation

🛠 Tech Stack

Framework: PyTorch
Model: Transformer Denoiser
Libraries: Torch, Matplotlib

📂 Project Structure

text-diffusion/
│── .gitkeep
│── diffusion text model.py # Core training + reconstruction script
│── train ce loss.png # Training loss curve (image)
│── requirements.txt # Dependencies
│── README.md # Documentation

⚡ Installation

git clone https://github.com/shubham-61291/non-transformer-ai-models.git

cd "text-diffusion"
pip install -r requirements.txt

▶️ Usage

python "diffusion text model.py"

This trains the model, logs training losses, and prints reconstruction outputs.

🖼 Demo

🔹 Training Loss Curve
![Training Loss](train%20ce%20loss.png)


🔹 Sample Reconstruction (Text Output)
Clean : i love dogs
Corrupted : <mask> <mask> dogs
Reconstructed: i love dogs

🔮 Future Enhancements

🔹 Extend to larger datasets (Wikipedia, BooksCorpus)
🔹 Add conditional diffusion for guided generation
🔹 Experiment with hybrid denoisers (Transformer + RNN)
🔹 Build a Gradio interface for interactive demos

👨‍💻 Author

Shubham Singh

📜 License

MIT License

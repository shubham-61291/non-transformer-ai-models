Autoencoder (MNIST) 📖 Overview

The Autoencoder (MNIST) is a deep learning model built using PyTorch that compresses and reconstructs handwritten digit images from the MNIST dataset. It demonstrates how unsupervised learning extracts compact latent features while maintaining reconstruction quality.

🚀 Key Features

✅ Unsupervised learning: Learns latent representations without labels.
✅ Efficient compression: Reduces 28×28 images to a 64-dimensional bottleneck.
✅ Accurate reconstruction: Decodes compressed features back into images.
✅ Visualization: Includes loss curve and reconstruction comparisons.
✅ Lightweight implementation: Simple, clean PyTorch pipeline.

🛠 Tech Stack

Framework: PyTorch
Dataset: MNIST (via torchvision)
Libraries: Torch, Torchvision, Matplotlib
Optimizer: AdamW
Loss: Binary Cross Entropy (BCE)

📂 Project Structure

autoencoder-mnist/
│── AE IMAGE MODEL.py # Core training + reconstruction script
│── output.png # Original vs reconstructed digits
│── training loss curve.png # Training loss curve
│── requirements.txt # Dependencies
│── README.md # Documentation

⚡ Installation

git clone https://github.com/shubham-61291/non-transformer-ai-models.git

cd "autoencoder-mnist"
pip install -r requirements.txt

▶️ Usage

python "AE IMAGE MODEL.py"

This will train the autoencoder on MNIST, plot the training loss, and generate reconstruction results.

🖼 Demo

🔹 Training Loss Curve
<img src="training%20loss%20curve.png" alt="Training Loss Curve" width="500"/>

🔹 Reconstructions
<img src="output.png" alt="Reconstruction Results" width="500"/>

🔮 Future Enhancements

🔹 Add Convolutional Autoencoder (ConvAE)
🔹 Extend to Variational Autoencoder (VAE/CVAE)
🔹 Implement denoising autoencoders
🔹 Build Gradio demo for deployment

👨‍💻 Author

Shubham Singh

📜 License

MIT License



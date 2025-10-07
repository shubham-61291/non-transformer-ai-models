# Conditional Variational Autoencoder (CVAE) 📖 Overview

The Conditional Variational Autoencoder (CVAE) is an extension of the VAE that conditions both the encoder and decoder on class labels. This implementation uses convolutional layers to learn meaningful latent representations of the MNIST dataset, enabling label-guided image generation.

## 🚀 Key Features
✅ Conditional generation: Outputs depend on digit labels (0–9)  
✅ Convolutional architecture: Learns richer image features  
✅ Reconstructions: Input vs reconstructed digit comparison  
✅ Class-conditional sampling: Generates digits conditioned on labels  
✅ Visualization: Saves both reconstructions and conditional samples  

## 🛠 Tech Stack
Framework: PyTorch  
Dataset: MNIST (via torchvision)  
Libraries: Torch, Torchvision, Matplotlib  
Optimizer: Adam  
Loss: Reconstruction + KL Divergence  

## 📂 Project Structure
cvae-mnist/  
│── cvaeimagemodel.py       # Core CVAE implementation and training  
│── output.png              # Reconstructions (input vs output)  
│── labels created.png      # Generated samples conditioned on labels  
│── requirements.txt        # Dependencies  
│── README.md               # Documentation  

## ⚡ Installation
git clone https://github.com/shubham-61291/non-transformer-ai-models.git  
cd "cvae-mnist"  
pip install -r requirements.txt  

## ▶️ Usage
python cvaeimagemodel.py  

This will train the CVAE and produce both reconstructions and conditional samples.

## 🖼 Demo
### 🔹 Reconstructions  
Input images (top) vs reconstructed outputs (bottom):  
![Reconstructions](output.png)

### 🔹 Class-Conditional Samples  
Generated digits 0–9 (rows represent class labels):  
![Conditional Samples](labels%20created.png)

## 🔮 Future Enhancements
🔹 Add deeper convolutional layers for improved fidelity  
🔹 Extend CVAE to color datasets (CIFAR-10, CelebA)  
🔹 Integrate with Gradio for an interactive demo  

## 👨‍💻 Author
Shubham Singh  

## 📜 License
MIT License

# Variational Autoencoder (MNIST) 📖 Overview
The Variational Autoencoder (VAE) on MNIST is a generative deep learning model built using PyTorch. It not only reconstructs input images but also learns a latent distribution, enabling the generation of new handwritten digit samples.

## 🚀 Key Features
✅ Variational Autoencoder with reparameterization trick.  
✅ Learns meaningful latent distribution from MNIST digits.  
✅ Can both reconstruct inputs and generate new samples.  
✅ Training visualization included (loss and outputs).  
✅ Lightweight, easy-to-train PyTorch pipeline.  

## 🛠 Tech Stack
Framework: PyTorch  
Dataset: MNIST (via torchvision)  
Libraries: Torch, Torchvision, Matplotlib  
Optimizer: AdamW  
Loss: Reconstruction Loss (BCE) + KL Divergence  

## 📂 Project Structure
vae-mnist/  
│── VAEIMAGE MODEL.py       # Core training + reconstruction script  
│── output.png              # Original vs reconstructed digits  
│── random output.png       # Randomly generated samples from latent space  
│── requirements.txt        # Dependencies  
│── README.md               # Documentation  

## ⚡ Installation
git clone https://github.com/shubham-61291/non-transformer-ai-models.git  
cd "vae-mnist"  
pip install -r requirements.txt  

## ▶️ Usage
python "VAEIMAGE MODEL.py"  

This will train the VAE on MNIST, save reconstruction results, and generate random outputs from the latent space.

## 🖼 Demo
🔹 **Reconstruction Results**  
<img src="output.png" alt="Reconstructed Digits" width="500"/>  

🔹 **Randomly Generated Samples**  
<img src="random%20output.png" alt="Randomly Generated Digits" width="500"/>  

## 🔮 Future Enhancements
🔹 Add Convolutional VAE (ConvVAE) for higher-quality results.  
🔹 Extend to Conditional VAE (CVAE) for label-guided generation.  
🔹 Train on complex datasets (CIFAR-10, CelebA).  
🔹 Deploy interactive Gradio app for sampling digits live.  

## 👨‍💻 Author
Shubham Singh

## 📜 License
MIT License

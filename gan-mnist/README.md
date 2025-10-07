# GAN (MNIST) 📖 Overview

The GAN (Generative Adversarial Network) is implemented in PyTorch to generate handwritten digits from the MNIST dataset. It consists of a Generator and Discriminator trained in an adversarial setup, demonstrating how GANs learn to create realistic samples from random noise.

---

## 🚀 Key Features
✅ Adversarial training with Generator & Discriminator  
✅ Learns to generate realistic MNIST-like digits  
✅ Progressive improvement across epochs  
✅ Visualization of outputs at multiple training stages  
✅ Training loss tracking for both Generator and Discriminator  

---

## 🛠 Tech Stack
Framework: PyTorch  
Dataset: MNIST (via torchvision)  
Libraries: Torch, Torchvision, Matplotlib  
Loss: Binary Cross Entropy (BCE)  
Optimizer: Adam  

---

## 📂 Project Structure
gan-mnist/  
│── gan model.py             # GAN training script  
│── after 10 epoch.png       # Generated samples after 10 epochs  
│── after 20 epoch.png       # Generated samples after 20 epochs  
│── after 30 epoch.png       # Generated samples after 30 epochs  
│── after 40 epoch.png       # Generated samples after 40 epochs  
│── after 50 epoch.png       # Generated samples after 50 epochs  
│── Gan training loss.png    # Training loss curves  
│── requirements.txt         # Dependencies  
│── README.md                # Documentation  

---

## ⚡ Installation
git clone https://github.com/shubham-61291/non-transformer-ai-models.git  
cd "gan-mnist"  
pip install -r requirements.txt  

---

## ▶️ Usage
python "gan model.py"  

This will train the GAN on MNIST and generate synthetic digit images after every few epochs.

---

## 🖼 Demo

🔹 **Training Loss**  
![Loss Curve](Gan%20training%20loss.png)

🔹 **Generated Samples (by Epochs)**  
Epoch 10:  
![Epoch 10](after%2010%20epoch.png)

Epoch 20:  
![Epoch 20](after%2020%20epoch.png)

Epoch 30:  
![Epoch 30](after%2030%20epoch.png)

Epoch 40:  
![Epoch 40](after%2040%20epoch.png)

Epoch 50:  
![Epoch 50](after%2050%20epoch.png)

---

## 🔮 Future Enhancements
🔹 Use Deep Convolutional GAN (DCGAN)  
🔹 Add conditional GAN (cGAN) for label-based generation  
🔹 Experiment with Wasserstein GAN (WGAN)  
🔹 Deploy with Gradio interface  

---

## 👨‍💻 Author
Shubham Singh 

---

## 📜 License
MIT License

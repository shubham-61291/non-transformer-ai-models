# DCGAN (MNIST) 📖 Overview

The Deep Convolutional GAN (DCGAN) is implemented in PyTorch to generate handwritten digits from the MNIST dataset. Unlike the vanilla GAN, this model uses convolutional and transpose-convolutional layers for stable training and improved image quality.

---

## 🚀 Key Features
✅ Convolutional Generator & Discriminator  
✅ Learns to generate realistic MNIST digits  
✅ Progressive outputs across epochs (5 → 20)  
✅ Training loss visualization  
✅ Stable adversarial training  

---

## 🛠 Tech Stack
Framework: PyTorch  
Dataset: MNIST (via torchvision)  
Libraries: Torch, Torchvision, Matplotlib  
Loss: Binary Cross Entropy (BCE)  
Optimizer: Adam  

---

## 📂 Project Structure
dcgan-mnist/  
│── DCGAN.py                 # DCGAN implementation and training script  
│── after 5 epoch.png        # Generated samples after 5 epochs  
│── after 10 epoch.png       # Generated samples after 10 epochs  
│── after 15 epoch.png       # Generated samples after 15 epochs  
│── after 20 epoch.png       # Generated samples after 20 epochs  
│── training loss.png        # Training loss curves  
│── requirements.txt         # Dependencies  
│── README.md                # Documentation  
│── .gitkeep                 # To track empty folder  

---

## ⚡ Installation
git clone https://github.com/shubham-61291/non-transformer-ai-models.git  
cd "dcgan-mnist"  
pip install -r requirements.txt  

---

## ▶️ Usage
python "DCGAN.py"  

This will train the DCGAN on MNIST and save generated digit images after every 5 epochs.

---

## 🖼 Demo

🔹 **Training Loss Curve**  
![Loss Curve](training%20loss.png)

🔹 **Generated Samples (by Epochs)**  
Epoch 5:  
![Epoch 5](after%205%20epoch.png)  

Epoch 10:  
![Epoch 10](after%2010%20epoch.png)  

Epoch 15:  
![Epoch 15](after%2015%20epoch.png)  

Epoch 20:  
![Epoch 20](after%2020%20epoch.png)  

---

## 🔮 Future Enhancements
🔹 Add Conditional DCGAN for label-based control  
🔹 Experiment with Wasserstein GAN (WGAN) for better stability  
🔹 Scale up to higher resolution datasets like CIFAR-10 or CelebA  
🔹 Integrate with Gradio for live digit generation  

---

## 👨‍💻 Author
Shubham Singh

---

## 📜 License
MIT License

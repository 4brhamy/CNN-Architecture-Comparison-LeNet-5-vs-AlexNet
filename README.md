# Assignment 3: Deep Learning Architectures (CNNs)
## A Comparative Study: LeNet-5 (1998) & AlexNet (2012) on CIFAR-10

**Student Name**: Abrham Yilma  
**Course**: Deep Learning / Advanced Computer Vision  

---

### 📌 Project Overview
This repository contains a theoretical and empirical comparative analysis of two landmark Convolutional Neural Networks (CNNs): **LeNet-5** and **AlexNet**. The evolution from LeNet-5 to AlexNet represents the story of scaling up in deep learning, driven by the availability of larger datasets, GPU compute scale, and innovative activation/regularization methods.

### 🎯 Objectives
* **Explain** the motivation behind LeNet-5 and AlexNet architectures.
* **Describe** the architectural innovations introduced by AlexNet compared to LeNet-5.
* **Implement** both deep learning models in PyTorch.
* **Train and Evaluate** the models on the realistic CIFAR-10 dataset.
* **Analyze** their strengths, weaknesses, computational tradeoffs, and evolutionary significance.

---

### 📁 Repository Contents
* `CNN Assignment LeNet vs AlexNet colab.ipynb`: The primary Google Colab notebook containing the PyTorch implementations, data preprocessing, training loops, and evaluation metrics.
* `LeNet5_vs_AlexNet_Presentation.pptx`: The slide deck summarizing the theoretical background, architectural paradigms, and training results.

---

### 🏗️ Architectural Paradigm Comparison

| Feature | LeNet-5 (1998) | AlexNet (2012) | Evolutionary Impact |
| :--- | :--- | :--- | :--- |
| **Input Dimensions** | 32 x 32 x 1 (Grayscale) | 224 x 224 x 3 (RGB Color) | Handles higher spatial resolution and rich color. |
| **Activation Function** | Sigmoid / Tanh | ReLU (Rectified Linear Unit) | Solves the vanishing gradient problem; 6x faster convergence. |
| **Pooling Mechanism** | Average Pooling | Overlapping Max Pooling | Reduces overfitting and preserves spatial representations. |
| **Regularization** | None (Weight decay only) | Dropout (0.5) & Data Augmentation | Prevents co-adaptation of neurons; crucial for scaling. |
| **Normalization** | None | Local Response Normalization (LRN) | Emulates lateral inhibition in biological brain cells. |
| **Depth & Parameters** | 7 layers, ~60K parameters | 8 layers, ~60M parameters | 1000x scale allows representation of highly complex features. |
| **Compute Target** | Single CPU | Dual-GPU Parallelization | Unlocks scaling parameters from 60K to 60M. |

---

### 📊 Dataset & Processing Strategy
To evaluate both models under similar conditions, this project utilizes the **CIFAR-10** dataset (60,000 color images across 10 balanced classes). 
* **LeNet-5**: Maintained the 32x32 spatial resolution but modified the first convolutional layer to accept 3-channel RGB input.
* **AlexNet**: Images were dynamically resized to 224x224 during dataloading to showcase standard AlexNet behavior.

---

### 🏆 Empirical Results

Both models were trained using the Adam optimizer (LeNet-5 LR: 0.001, AlexNet LR: 0.0001) for 5 epochs on a Tesla T4 GPU.

**Convergence & Accuracy (Epoch 5):**
* **AlexNet**: 78.08% Test Accuracy | 0.5577 Loss.
* **LeNet-5**: 55.69% Test Accuracy | 1.2130 Loss.
* *AlexNet achieved a +22.39% absolute gain in accuracy and over 2.1x lower loss*.

**Computational Time:**
* **LeNet-5**: 13.71 seconds / epoch.
* **AlexNet**: 133.06 seconds / epoch.
* *Tradeoff: AlexNet is approximately 9.7x slower to train due to spatial resize workloads and massive parameter scaling*.

**Class Performance Highlights:**
* **AlexNet** achieved its highest precision on `ship` (94%) and highest recall on `truck` (91%). 
* **LeNet-5** struggled heavily with complex classes like `cat` (42% precision) and `dog` (54% precision), whereas AlexNet significantly boosted these metrics (64% and 74% precision, respectively).

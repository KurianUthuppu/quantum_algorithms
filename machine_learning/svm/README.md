# Quantum Kernel SVM vs Classical RBF-SVM: A Comparative Study

## Learning Objectives

By completing this notebook, you will:

✅ Understand differences between classical and quantum kernels  
✅ Implement and train quantum kernels using QKA  
✅ Compare performance across three approaches quantitatively  
✅ Analyze kernel matrices and decision boundaries  
✅ Identify scenarios where quantum kernels provide advantages

## 1. Introduction

### 1.1 Overview

Support Vector Machines (SVMs) find optimal hyperplanes in feature space to separate different classes. The **kernel function** determines how data points are mapped into higher-dimensional space where linear separation becomes possible.

This notebook compares three approaches:

- **Classical RBF Kernel SVM**: Traditional radial basis function approach
- **Static Quantum Kernel SVM**: Fixed quantum feature maps
- **Trainable Quantum Kernel SVM**: Optimized using Quantum Kernel Alignment (QKA)

---

### 1.2 Classical vs Quantum Kernels

#### Classical RBF Kernel

$$K_{\text{RBF}}(\mathbf{x}, \mathbf{y}) = \exp\left(-\gamma \|\mathbf{x} - \mathbf{y}\|^2\right)$$

**Properties:**

- Maps data to infinite-dimensional Hilbert space
- Computationally efficient and well-understood
- Controlled by hyperparameter $\gamma$

#### Quantum Kernel

$$K_{\text{quantum}}(\mathbf{x}, \mathbf{y}) = |\langle\phi(\mathbf{y})|\phi(\mathbf{x})\rangle|^2$$

where $|\phi(\mathbf{x})\rangle = U_{\phi}(\mathbf{x})|0\rangle^{\otimes n}$ is the quantum state from applying feature map $U_{\phi}(\mathbf{x})$ to the initial state.

**Properties:**

- Exploits quantum superposition and entanglement
- Accesses exponentially large Hilbert spaces
- Potential advantage for specific problem structures

---

### 1.3 Quantum Kernel Alignment (QKA)

While static quantum kernels show promise, **Quantum Kernel Alignment (QKA)** optimizes the parameters $\boldsymbol{\theta}$ of the quantum feature map $U_{\phi}(\mathbf{x}; \boldsymbol{\theta})$ to improve performance on the given dataset.

#### How QKA Works

QKA maximizes alignment between the quantum kernel matrix and the ideal kernel derived from class labels:

$$\hat{A}(K, K_{\text{ideal}}) = \frac{\langle K, K_{\text{ideal}} \rangle_F}{\sqrt{\langle K, K \rangle_F \langle K_{\text{ideal}}, K_{\text{ideal}} \rangle_F}}$$

where $\langle \cdot, \cdot \rangle_F$ is the Frobenius inner product.

**Key Benefits:**

- Iteratively adapts the kernel to the dataset
- Converges to maximum SVM margin
- No repeated SVM training during optimization
- Efficient gradient-based parameter updates

**Trainable Parameters:**

- Rotation angles in quantum gates
- Entanglement patterns
- Feature encoding strategies

**References:**

- [Covariant quantum kernels for data with group structure](https://arxiv.org/abs/2105.03406)
- [Quantum Kernel Training Toolkit Documentation](https://qiskit-community.github.io/qiskit-machine-learning/tutorials/03_quantum_kernel.html)

---

### 1.4 Three-Way Comparison

| Approach                    | Kernel Type          | Optimization                  | Quantum Resources |
| --------------------------- | -------------------- | ----------------------------- | ----------------- |
| **Classical RBF**           | Fixed RBF            | Hyperparameter tuning (C, γ)  | None              |
| **Static Quantum**          | Fixed feature map    | Feature map                   | Moderate          |
| **Trainable Quantum (QKA)** | Adaptive feature map | Feature map + hyperparameters | High              |

---

### 1.5 Workflow Overview

The Quantum Kernel Training (QKT) toolkit provides a structured workflow:

```
1. Prepare Dataset
   ↓
2. Define Parametrized Quantum Feature Map
   ↓
3. Setup TrainableFidelityQuantumKernel
   ↓
4. Configure QuantumKernelTrainer with QKA Loss
   ↓
5. Train Kernel Parameters using fit() method
   ↓
6. Use Trained Kernel in SVC
   ↓
7. Evaluate and Compare Performance
```

**Key Components:**

- **TrainableFidelityQuantumKernel**: Quantum kernel with trainable parameters
- **QuantumKernelTrainer**: Orchestrates the training process
- **QKA Loss Function**: Computes kernel alignment objective

---

## 2. Knowledge Prerequisites

- Basic understanding of Support Vector Machines
- Familiarity with quantum computing concepts (qubits, gates, circuits)
- Python and machine learning fundamentals

---

## 3. Installation

```bash
pip install -r requirements.txt
```

---

Let's begin! 🚀

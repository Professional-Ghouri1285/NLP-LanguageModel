# NLP-LanguageModel
Repsository which contains my own implementation of a language model based on the transformer model described in the Attention is all you need paper.

# From Scratch to Distributed GPT (C++)

This repository documents my complete journey of understanding and building a GPT-like model **from absolute fundamentals to a distributed system**.

The goal is not just to *use* transformers — but to **understand, implement, and scale them from scratch**.

---

# 📌 Project Overview

This project is divided into multiple stages:

1. **Conceptual Understanding (By Hand)**
2. **Mathematical Breakdown of GPT**
3. **Minimal C++ Implementation**
4. **Training Loop + Text Generation**
5. **Distributed LLM Architecture (Android + Linux Master)**
6. **(Future) Pretrained Weights Integration**

---

# 🧩 Stage 1 — Understanding Transformers (From Scratch)

* What is a token?
* What are embeddings?
* What is attention?
* Why masking is needed (autoregressive models)
* Step-by-step manual forward pass (with small numbers)
* Step-by-step gradient update (by hand)

---

# 🧮 Stage 2 — GPT Math (Solved Manually)

Implemented on paper:

* Token → embedding → positional encoding
* Q, K, V computation
* Scaled dot-product attention
* Masking (causal)
* Softmax probabilities
* Cross-entropy loss
* Gradient computation
* Parameter update (SGD)

Goal: **Understand every number inside GPT**

---

# ⚙️ Stage 3 — C++ Implementation (From Scratch)

No frameworks. No libraries. Only:

* `vector`
* basic matrix operations

## Implemented Components

* Matrix struct
* Matrix multiplication
* Softmax
* ReLU
* Layer Normalization
* Token embeddings
* Positional embeddings
* Masked self-attention
* Feed-forward network
* Final linear projection

## Constraints

* No CUDA
* No heavy STL usage
* Fully manual math implementation

---

# 🔁 Stage 4 — Training & Generation

(To be completed)

* Cross-entropy loss
* Backpropagation
* SGD updates
* Training loop
* Autoregressive text generation

Example goal:

```
Input:  "hel"
Output: "hello"
```

---

# 🌐 Stage 5 — Distributed LLM Architecture

Goal:

> Run a single LLM across multiple devices.

## Setup

* 4 Android devices (workers)
* 1 Linux machine (master)

## Constraints

* ≤ 500 MB RAM per device
* ≤ 1 GB storage per device

---

## Architecture Design

### Sequential (Master Only)

* Token generation loop
* Layer stacking
* Softmax
* Sampling next token

---

### Parallel (Across Android Devices)

* Matrix multiplications
* Q, K, V projections
* Attention computations
* Feed-forward layers

---

## Parallelization Strategy

### Tensor Parallelism (Weight Sharding)

Each device stores:

* 1/4 of model weights

Each device computes:

* Partial matrix outputs

Master:

* Aggregates results
* Performs softmax + sampling

---

## Communication Flow

For each token:

1. Master sends activations
2. Workers compute partial outputs
3. Workers return results
4. Master aggregates
5. Master generates next token

---

# 📦 Stage 6 — Pretrained Weights (Planned)

* Load existing GPT weights
* Convert to custom C++ format
* Apply quantization (FP16 / INT8)
* Fit into mobile constraints

---

# 🎯 Goals of This Repo

* Understand transformers deeply (not just use them)
* Build GPT-like model without libraries
* Implement training manually
* Scale model across multiple devices
* Explore real-world system constraints

---

# 📁 Structure (Planned)

```
/notes/          → handwritten math, derivations
/cpp/            → core implementation
/dataset/        → input.txt (training data)
/distributed/    → architecture design + simulation
/utils/          → matrix operations, helpers
```

---

# 🚀 Future Work

* Multi-head attention
* KV cache optimization
* Efficient communication between devices
* Real-time distributed inference
* Optimization for mobile devices

---

# 📖 Why This Project?

Most people:

* Use libraries
* Treat transformers as black boxes

This project:

* Opens the black box
* Builds everything from scratch
* Connects math → code → systems

---

# ⚠️ Disclaimer

This is an educational project focused on **understanding and system design**, not production performance.

---

# 🧠 Author

Built as a deep learning + systems learning journey.

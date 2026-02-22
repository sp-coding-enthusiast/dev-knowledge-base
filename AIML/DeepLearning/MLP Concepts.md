# Multi‑Layer Perceptron (MLP) — Layman Explanation + All Formulas

## 1. What is an MLP? (Simple View)

A Multi‑Layer Perceptron is a basic type of neural network made of layers of connected “neurons.”

Think of it like a factory:

* Input layer → raw material (data)
* Hidden layer → processing
* Output layer → final decision

Example (digit recognition):

* Input: image pixels
* Hidden: detect shapes/edges
* Output: which digit (0–9)

---

# 2. How a Single Neuron Works (Layman)

A neuron:

1. Looks at inputs
2. Gives each input importance (weight)
3. Adds them up
4. Adds a bias (adjustment)
5. Passes through activation (decision rule)

Real‑life analogy:
Choosing a house:

* price × importance
* location × importance
* size × importance

- personal bias
  → final score

---

# 3. Neuron Math (Formula)

Weighted sum:

z = x·w + b

Expanded:

z = x1w1 + x2w2 + … + xnwn + b

Activation output:

a = σ(z)

Where:

* x = inputs
* w = weights
* b = bias
* σ = activation function

---

# 4. Activation Function (Layman)

Activation decides whether a neuron should “fire.”

Example: ReLU

* positive → keep
* negative → 0

Why needed?
Without activation, network becomes just linear math and cannot learn complex patterns.

---

# 5. ReLU Formula

ReLU(z) = max(0, z)

---

# 6. MLP Forward Pass (Layman)

Data flows layer by layer:

input → hidden → output

Each layer:

* multiply by weights
* add bias
* apply activation

---

# 7. MLP Forward Pass Formulas

Hidden layer:

h = ReLU(x W1^T + b1)

Output layer (logits):

y = h W2^T + b2

Where:

* x = input vector
* W1, W2 = weight matrices
* b1, b2 = biases
* h = hidden activations
* y = raw outputs (logits)

---

# 8. Softmax (Convert Scores to Probabilities)

The network outputs scores for each class.
Softmax converts them into probabilities that sum to 1.

Example:
[2.0, 1.0, 0.1] → [0.65, 0.24, 0.11]

---

# 9. Softmax Formula

softmax(yi) = exp(yi) / Σj exp(yj)

---

# 10. Loss Function (Layman)

Loss measures how wrong predictions are.

If predicted digit ≠ true digit → loss high
If correct → loss low

Used to train the model.

---

# 11. Cross‑Entropy Loss Formula

L = − Σi ti log(pi)

Where:

* ti = true label (one‑hot)
* pi = predicted probability

---

# 12. Training Process (Layman)

Training repeats:

1. Predict
2. Measure error
3. Adjust weights

Like learning from mistakes.

---

# 13. Gradient Descent Update Rule

w_new = w_old − η ∇L

Where:

* η = learning rate
* ∇L = gradient of loss

---

# 14. Mini‑Batch Training

Instead of whole dataset, use small batches.

Example:
1000 images → batches of 32

Why?

* faster
* less memory
* stable learning

---

# 15. SGD Optimizer Formula

θ = θ − η ∇θ L

Where:

* θ = model parameters (weights, bias)

---

# 16. Prediction (Classification)

Choose class with highest probability.

Formula:

class = argmax(softmax(y))

---

# 17. Accuracy Formula

accuracy = correct_predictions / total_samples

---

# 18. Complete MLP Pipeline (Layman)

Image → flatten → neuron math → ReLU → neuron math → softmax → predicted digit

---

# 19. Key Concepts Summary (Simple)

* Neuron = weighted decision maker
* Layer = group of neurons
* Activation = non‑linearity
* Softmax = probabilities
* Loss = error measure
* Gradient descent = learning rule
* MLP = stacked neurons

---

# 20. All Formulas List (Quick Reference)

Neuron:
z = x·w + b

a = σ(z)

ReLU:
ReLU(z) = max(0, z)

Hidden layer:
h = ReLU(x W1^T + b1)

Output:
y = h W2^T + b2

Softmax:
softmax(yi) = exp(yi) / Σj exp(yj)

Cross‑entropy:
L = − Σi ti log(pi)

Gradient descent:
w = w − η ∇L

SGD:
θ = θ − η ∇θ L

Prediction:
class = argmax(softmax(y))

Accuracy:
accuracy = correct / total

---

# Final Intuition

An MLP learns by repeatedly:

* making predictions
* measuring mistakes
* adjusting connections

Just like a student improving with practice.

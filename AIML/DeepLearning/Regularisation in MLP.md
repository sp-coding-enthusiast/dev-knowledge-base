# Regularisation in MLP — Concepts + Formulas + Examples + Interview Q&A

## 🧠 Idea in Plain English

Imagine you are preparing for an exam.

* If you study **too little**, you fail → *underfitting*
* If you study **just right**, you understand concepts → *good generalization*
* If you memorize only past questions**, you score on practice but fail new questions → *overfitting*

**Early stopping = stop studying at the right time before memorization starts.**

---

## 📊 What Happens During Training

When we train a neural network, we track two errors:

* **Training error** → how well model fits training data
* **Validation error** → how well model works on unseen data

Typical pattern:

1. Start → both errors high
2. Training → both decrease
3. Over-training → training ↓ but validation ↑ ❗

That increase in validation error = model starts memorizing.

👉 **Early stopping rule:**
Stop training when validation error starts increasing.

---

## 🎯 Real‑Life Example

### Example 1 — Exam Preparation

* Day 1–5 → learning concepts → performance improves everywhere
* Day 6–10 → memorizing answers → practice improves, new questions worse

Teacher says: *"Stop here — you’re ready."*

That is early stopping.

---

### Example 2 — Face Recognition App

Training model to recognize people.

* Early training → learns general face features
* Later training → memorizes training photos
* Result → fails on new photos

Stopping earlier → works on new faces.

---

## 📈 Visual Intuition

Training vs Validation Error Curve:

```
Error
│\        Validation error ↑
│ \      /
│  \    /
│   \  /
│    \/
│    /\
│   /  \  Training error ↓
│  /    \
│ /      \
└────────────── Epochs
        ↑
   Stop here
```

---

## ⚙️ How Early Stopping Works in Practice

During training:

1. Train 1 epoch
2. Check validation error
3. Save best model
4. Repeat
5. If validation error increases for few epochs → stop

This patience window avoids stopping due to noise.

---

## ❗ Why It Prevents Overfitting

If training continues after validation worsens:

* Model memorizes training data
* Generalization drops
* Performance on real data decreases

Early stopping freezes model at best generalization point.

---

## 🚀 Key Advantages

* Simple
* No math changes
* Works with any model
* Saves training time
* Improves real‑world accuracy

---

# Teaching Neural Networks to Recognize Visual Patterns (Layman)

Images are difficult because they contain:

* shapes
* textures
* edges
* colors
* spatial structure

Neural networks learn visuals using **layers that detect patterns**.

---

## 🧩 How Pattern Learning Happens

Think of it like human vision:

1. See edges
2. Combine edges → shapes
3. Combine shapes → objects

Neural networks do same hierarchy:

* Layer 1 → edges
* Layer 2 → corners/textures
* Layer 3 → parts (eyes, wheels)
* Layer 4 → objects (face, car)

---

## 📷 Example — Cat Recognition

Training images of cats.

Network gradually learns:

* whisker lines
* triangular ears
* eye shapes
* fur texture

Then detects cat in new image.

---

# 🧪 Interview Questions and Answers

## Q1. What is early stopping?

**Answer:**
Early stopping is a technique where training is stopped when validation error starts increasing, preventing overfitting and preserving the best generalizing model.

---

## Q2. Why not train until training error is minimum?

**Answer:**
Because training error can decrease while validation error increases, meaning the model is memorizing rather than generalizing.

---

## Q3. Difference between validation set and test set?

**Answer:**

* Validation set → used during training to tune/stop model
* Test set → used only once after training for final evaluation

---

## Q4. How do you implement early stopping?

**Answer:**
Monitor validation loss each epoch and stop training if it does not improve for a fixed number of epochs (patience).

---

## Q5. What is patience in early stopping?

**Answer:**
Number of epochs to wait after validation stops improving before stopping training.

---

## Q6. Is early stopping regularization?

**Answer:**
It is not a mathematical regularization term but acts as implicit regularization by preventing over‑training.

---

## Q7. What happens if you ignore early stopping?

**Answer:**
Model overfits training data and performs poorly on unseen data.

---

## Q8. Why save the best model during early stopping?

**Answer:**
Because later epochs may degrade performance; saving ensures the best validation model is retained.

---

## Q9. How does early stopping affect training time?

**Answer:**
It reduces training time by stopping unnecessary epochs.

---

## Q10. Can early stopping be used with any neural network?

**Answer:**
Yes, it is model‑agnostic and works with any training process using validation data.

---

# 📐 Mathematical Formulas Behind the Concepts

## 1️⃣ L2 Regularisation (Weight Decay)

Adds penalty for large weights to the loss.

**Regularised loss:**

L_total = L_data + λ sum(w^2)

Where:

* L_data = original loss (e.g., cross‑entropy)
* λ = regularisation strength
* w = model weights

**Effect on update:**

w = w − η (∂L/∂w + 2λw)

Meaning weights are pushed toward zero → simpler model → less overfitting.

---

## 2️⃣ Dropout

Randomly turns off neurons during training.

**Forward during training:**

h_tilde = m ⊙ h

Where:

* h = neuron activations
* m ~ Bernoulli(p) mask
* ⊙ = element‑wise multiply
* p = keep probability

**Inference scaling:**

h_test = p · h

So expected activation stays same.

---

## 3️⃣ Batch Normalisation

Normalises layer activations within a batch.

**Step 1 — Normalize:**

x_hat = (x − mu_B) / sqrt(var_B + eps)

**Step 2 — Scale & shift:**

y = gamma x_hat + beta

Where:

* mu_B = batch mean
* var_B = batch variance
* gamma, beta = learnable parameters

Purpose: stable gradients + faster training + regularisation effect.

---

## 4️⃣ Early Stopping (Validation‑based)

Stops training when validation loss increases.

**Criterion:**

Stop at epoch t if:

L_val(t) > L_val(t−k)

for k consecutive epochs (patience).

**Best model:**

theta* = argmin_t L_val(t)

Training halts at epoch of minimum validation loss.

---

# ✅ Summary

Early stopping = stop training when validation error increases.

It prevents memorization and keeps the model generalizable.

Neural networks learn visual patterns by building hierarchical features from edges → shapes → objects.

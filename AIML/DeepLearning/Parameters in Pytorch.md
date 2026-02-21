# Parameters in PyTorch — Concepts & Formulas

## Overview
This document explains the key concepts and formulas from the **Parameters in Torch** notebook in clear, simple terms suitable for learning and interviews.

---

# Parameters in Torch

### Overview
In this session, we explore **parameters in PyTorch** — the fundamental building blocks that store and update the weights of neural networks. You will learn how to create parameters, understand their role in training, and see how they fit inside an **`nn.Module`** to form a model. We will also visualize how these parameters change during learning.  

### Agenda
1. **What are Parameters?** → understanding the difference between tensors and parameters.  
2. **Creating Parameters** → using `torch.nn.Parameter`.  
3. **Placing Parameters inside an `nn.Module`** → turning them into a model.  
4. **Parameters in Layers** → exploring weights and biases inside `nn.Linear`, etc.  

### Key Takeaway
By the end of this session, you will understand what parameters are, how they become part of a model through **`nn.Module`**, and how to inspect, modify, and visualize them in action.  

## Setup & Device

```python
import torch
import torch.nn as nn
import random

# Reproducibility
seed = 42
random.seed(seed)
torch.manual_seed(seed)

# Device
device = torch.device("cuda" if torch.cuda.is_available() else "cpu")
device
```

## What are Parameters?

- A **Tensor** is just a container for numbers.  
- A **Parameter** is a *special tensor* that PyTorch marks as **learnable**.  
- During training, these parameters are the values that **get updated** so the model improves.  
- We put parameters inside an **`nn.Module`** → this becomes our **model**.  

Think of it this way:  
- Tensor = plain notebook page (just holds info).  
- Parameter = page with a sticky note (“important, revise!”) — PyTorch knows to keep track of it.

## Creating Parameters

- A parameter is created by wrapping a **tensor** with `nn.Parameter`.  
- This tells PyTorch: *“treat this tensor as learnable.”*  
- By default, Parameters are designed to be updated during training.  
- We usually store them inside an **`nn.Module`**, so they become part of a model.

```python
import torch
import torch.nn as nn

# A normal tensor
t = torch.tensor([1.0, 2.0, 3.0])
print("Tensor:", t)
print()

# A parameter (learnable tensor)
p = nn.Parameter(torch.tensor([1.0, 2.0, 3.0]))
print("Parameter:\n", p)
```

### Creating a simple Neuron

```python
# Minimal model with one weight and one bias as Parameters

class SingleNeuron(nn.Module):
    def __init__(self):
        super().__init__()
        self.w = nn.Parameter(torch.tensor([0.1]))
        self.b = nn.Parameter(torch.tensor([0.0]))

    # forward is what actually computes the output, given the output, here you define how or what flow to be considered
    def forward(self, x):
        return self.w * x + self.b
```

```python
# Instantiate model
neuron = SingleNeuron()
print("Model parameters:")
for name, param in neuron.named_parameters():
    print(name, ":", param.shape)
```

## Using the Model Once

Once we have Parameters inside a model, we can **give an input** and get an **output**.

- In our custom neuron: `y = w*x + b`

```python
# Give an input
x = torch.tensor([2.0])
y = neuron(x)

print("Input:", x.item(), " → Output:", y.item())
```

## Creating Parameters with Built-in Layers

So far we created our own Parameters (`w`, `b`).  
But in practice, PyTorch layers like `nn.Linear` **already come with Parameters inside**:
- `weight`
- `bias`

These are the same kind of Parameters we made by hand — just managed automatically.

```python
import torch
import torch.nn as nn

# A fully connected layer: 4 inputs → 3 outputs (digits)
layer = nn.Linear(in_features=4, out_features=3)

print("Parameters in nn.Linear:")
for name, param in layer.named_parameters():
    print(name, ":", param.shape)
```

```python
# Input vector of size 4
x = torch.randn(1, 4)   # batch size = 1, 4 features
y = layer(x)

print("Input shape:", x.shape)
print("Output shape:", y.shape)
print("Output:", y)
```

### Key Point
Parameters define how the model turns **inputs into outputs**.  
By “using the model once,” we’re simply giving it data and seeing the result.  


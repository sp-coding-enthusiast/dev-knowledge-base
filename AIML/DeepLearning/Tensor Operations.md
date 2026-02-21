# Tensors and Tensor Operations (PyTorch)

## 1. What is a Tensor?
A **tensor** is a multi-dimensional array used to represent data such as scalars (0D), vectors (1D), matrices (2D), and higher-dimensional data.

```python
import torch
x = torch.tensor([1, 2, 3])
```

## 2. Tensor Data Types
PyTorch supports multiple dtypes like `int`, `float`, `double`.

```python
torch.tensor([1,2,3], dtype=torch.float32)
```

## 3. Moving Tensors to GPU
To accelerate computation, tensors can be moved to GPU.

```python
device = torch.device("cuda" if torch.cuda.is_available() else "cpu")
x = x.to(device)
```

## 4. Basic Tensor Operations
### Arithmetic Operations
Element-wise addition, subtraction, multiplication.

```python
a = torch.tensor([1,2])
b = torch.tensor([3,4])
a + b
```

### Matrix Multiplication
```python
A = torch.randn(2,3)
B = torch.randn(3,2)
torch.matmul(A, B)
```

### Dot Product
```python
torch.dot(torch.tensor([1.,2.]), torch.tensor([3.,4.]))
```

### Transpose
```python
A.T
```

### Slope Approximation
First-order difference approximates slope.

```python
x = torch.tensor([1.,2.,4.])
x[1:] - x[:-1]
```

## 5. Tensor Functions
### Reshaping
```python
x = torch.arange(6)
x.view(2,3)
```

### Slicing and Indexing
```python
x[0:2]
```

## 6. Neural Networks with Tensors
### Multi-Layer Perceptron (MLP)
```python
import torch.nn as nn

model = nn.Sequential(
    nn.Linear(784, 128),
    nn.ReLU(),
    nn.Linear(128, 10)
)
```

## 7. Training Loop
```python
loss_fn = nn.CrossEntropyLoss()
optimizer = torch.optim.Adam(model.parameters())

for data, target in train_loader:
    optimizer.zero_grad()
    output = model(data)
    loss = loss_fn(output, target)
    loss.backward()
    optimizer.step()
```

## 8. Regularisation and Normalisation
### Dropout
```python
nn.Dropout(0.5)
```

### Batch Normalisation
```python
nn.BatchNorm1d(128)
```

## 9. Evaluation
```python
model.eval()
```

## Key Takeaways
- Tensors are the core data structure in PyTorch
- GPU acceleration improves performance
- Tensor operations enable neural network training

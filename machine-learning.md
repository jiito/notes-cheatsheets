# Machine/Deep Learning

**A neural network approximates a function.**

### Energy Based Models

[Reference](https://deepai.org/machine-learning-glossary-and-terms/energy-based-models#:~:text=In%20the%20same%20way%2C%20machine,quality%20of%20the%20energy%20functions.)

[Cross Entropy Loss](https://machinelearningmastery.com/cross-entropy-for-machine-learning/)

### CNNs

Deep learning. Combinations of combinations.
[Computerfile Video](https://www.youtube.com/watch?v=py5byOOHZM8)
Downsample the space.

- Replacing each node with a kernel convolution.
- Convolution - takes a different kernel and output a single channel

### Transformers

### JAX

- JAX is accelerated NumPy designed to be a functional programming paradigm
- because of this functional programming paradigm, JAX data strucutres are not able to be modified in place and functions should not have side effects.
- It allows you to transform functions easily and can be run on many backends (CPU, GPU, TPU)
- `jax.grad` takes a numerical function and computes the gradient

  - it will only work on functions with scalar outputs
  - by default this will find the gradient with respect to the first variable
    most commonly, the loss function using JAX in machine learning looks like

  ```python
  def loss_fn(params, data):
  ...
  grads = jax.grad(loss_fn)(params, data_batch)
  ```

  This saves us from writing long argument lists. JAX uses a data structure called 'pytrees'

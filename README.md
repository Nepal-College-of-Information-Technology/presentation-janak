# Hopfield Neural Network
*Last Updated: 13 Mar, 2024*

## Discrete Hopfield Network

The Hopfield Neural Networks, invented by Dr. John J. Hopfield, consist of one layer of ‘n’ fully connected recurrent neurons. They are commonly used for auto-association and optimization tasks. The network operates through a converging interactive process and exhibits different behavior compared to traditional neural networks.

### Structure & Architecture

- Each neuron has an inverting and a non-inverting output.
- Fully connected: the output of each neuron serves as an input to all other neurons but not to itself.

### Weight Properties

- Symmetric weights: wij = wji.
- Self-connections are absent: wii = 0.

### Training Algorithm

To store a set of input patterns S(p) [p = 1 to P], where S(p) = S1(p), ..., Si(p), ..., Sn(p), the weight matrix is calculated as follows:

- **Binary Patterns:**
  wij = ∑p=1P [2si(p) - 1][2sj(p) - 1] (for all i ≠ j)

- **Bipolar Patterns:**
  wij = ∑p=1P [si(p) sj(p)] (where wij = 0 for all i = j)

### Steps in Training

1. **Initialize weights** (wij) using the training algorithm.
2. For each input vector yi:
   - Set initial activations of the network equal to the external input vector x.
   - Calculate the total input yin of the network: yini = xi + ∑j [yj wji].
   - Apply activation: yi = {1 if yin > θi, yi if yin = θi, 0 if yin < θi} (where θi is typically 0).
   - Feedback the obtained output yi to all other units to update activation vectors.
3. Test the network for convergence.

### Example Problem

Consider a Discrete Hopfield Network with a stored input vector x = [1 1 1 -1] (bipolar). Test the network with a modified input vector [0 0 1 0], with missing entries in the first and second components.

Given the weight matrix initialization and subsequent steps, determine if convergence to the original input vector is achieved.

## Continuous Hopfield Network

Unlike discrete Hopfield networks, here the time parameter is treated as continuous. Outputs range between 0 and 1, facilitating solutions to constrained optimization and associative memory problems.

### Output and Energy Function

- Output vi = g(ui), where vi is the output and ui is the internal activity of a node.
- Energy function E = 0.5 ∑i=1n ∑j=1n wij vi vj + ∑i=1n θi vi.
- Convergence condition: dE/dt ≤ 0.
- Activity equation: dui/dt = -ui/τ + ∑j wij vj + θi.


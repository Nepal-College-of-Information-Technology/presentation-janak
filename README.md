# Hopfield Neural Network
*Last Updated: 13 Mar, 2024*

## Discrete Hopfield Network

The Hopfield Neural Networks, invented by Dr. John J. Hopfield, consist of one layer of ‘n’ fully connected recurrent neurons. They are commonly used for auto-association and optimization tasks. The network operates through a converging interactive process and exhibits different behavior compared to traditional neural networks.

### Structure & Architecture

- Each neuron has an inverting and a non-inverting output.
- Fully connected: the output of each neuron serves as an input to all other neurons but not to itself.

### Weight Properties

- Symmetric weights: \( w_{ij} = w_{ji} \).
- Self-connections are absent: \( w_{ii} = 0 \).

### Training Algorithm

To store a set of input patterns \( S(p) \) [\( p = 1 \) to \( P \)], where \( S(p) = S_1(p), \ldots, S_i(p), \ldots, S_n(p) \), the weight matrix is calculated as follows:

- **Binary Patterns:**
  \[ w_{ij} = \sum_{p=1}^{P} [2S_i(p) - 1][2S_j(p) - 1] \quad \text{(for all \( i \neq j \))} \]

- **Bipolar Patterns:**
  \[ w_{ij} = \sum_{p=1}^{P} S_i(p) S_j(p) \quad \text{(where \( w_{ii} = 0 \) for all \( i = j \))} \]

### Steps in Training

1. **Initialize weights** (\( w_{ij} \)) using the training algorithm.
2. For each input vector \( y_i \):
   - Set initial activations of the network equal to the external input vector \( x \).
   - Calculate the total input \( y_{in} \) of the network: \( y_{in} = x_i + \sum_{j} [y_j w_{ji}] \).
   - Apply activation: \( y_i = \begin{cases} 1 & \text{if } y_{in} > \theta_i \\ y_i & \text{if } y_{in} = \theta_i \\ 0 & \text{if } y_{in} < \theta_i \end{cases} \) (where \( \theta_i \) is typically 0).
   - Feedback the obtained output \( y_i \) to all other units to update activation vectors.
3. Test the network for convergence.

### Example Problem

Consider a Discrete Hopfield Network with a stored input vector \( x = [1, 1, 1, -1] \) (bipolar). Test the network with a modified input vector [0, 0, 1, 0], with missing entries in the first and second components.

Given the weight matrix initialization and subsequent steps, determine if convergence to the original input vector is achieved.

## Continuous Hopfield Network

Unlike discrete Hopfield networks, here the time parameter is treated as continuous. Outputs range between 0 and 1, facilitating solutions to constrained optimization and associative memory problems.

### Output and Energy Function

- Output \( v_i = g(u_i) \), where \( v_i \) is the output and \( u_i \) is the internal activity of a node.
- Energy function \( E = 0.5 \sum_{i=1}^{n} \sum_{j=1}^{n} w_{ij} v_i v_j + \sum_{i=1}^{n} \theta_i v_i \).
- Convergence condition: \( \frac{dE}{dt} \leq 0 \).
- Activity equation: \( \frac{du_i}{dt} = -\frac{u_i}{\tau} + \sum_{j} w_{ij} v_j + \theta_i \).


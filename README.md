# Hopfield Neural Network

**Last Updated:** 13 Mar, 2024

Hopfield Neural Networks, invented by Dr. John J. Hopfield, consist of one layer of 'n' fully connected recurrent neurons. They are used primarily for auto-association and optimization tasks. The network operates using a converging interactive process and generates distinct responses compared to traditional neural networks.

## Discrete Hopfield Network

It is a fully interconnected neural network where each unit is connected to every other unit. The network operates in a discrete manner, providing finite distinct outputs, typically binary (0/1) or bipolar (-1/1). The weight matrix in this network is symmetric with properties:
1. \( w_{ij} = w_{ji} \)
2. \( w_{ii} = 0 \)

### Structure & Architecture of Hopfield Network

- Each neuron has an inverting and non-inverting output.
- Being fully connected, the output of each neuron serves as input to all other neurons except itself.

### Training Algorithm

For storing a set of input patterns \( S(p) \) where \( p = 1 \) to \( P \), the weight matrix is computed as follows:

- For binary patterns:
\[ w_{ij} = \sum_{p=1}^{P} [2s_i(p) - 1][2s_j(p) - 1] \quad \text{(where } w_{ij} = w_{ji} \text{ and } i \neq j \text{)} \]

- For bipolar patterns:
\[ w_{ij} = \sum_{p=1}^{P} [s_i(p) s_j(p)] \quad \text{(where } w_{ij} = 0 \text{ for all } i = j \text{)} \]

Steps involved in the training of a Hopfield Network:
1. Initialize weights \( w_{ij} \) using the training algorithm.
2. For each input vector \( y_i \), perform steps 3-7.
3. Set the initial activations of the network equal to the external input vector \( x \):
\[ y_i = x_i \quad \text{for } i = 1 \text{ to } n \]

4. For each vector \( y_i \), perform steps 5-7.
5. Calculate the total input of the network \( y_{in} \):
\[ y_{in, i} = x_i + \sum_j [y_j w_{ji}] \]

6. Apply activation over the total input to calculate the output:
\[ y_i = \begin{cases} 
1 & \text{if } y_{in} > \theta_i \\
y_i & \text{if } y_{in} = \theta_i \\
0 & \text{if } y_{in} < \theta_i 
\end{cases} \]
(where \( \theta_i \) (threshold) is normally taken as 0)

7. Update the activation vectors by feeding back the obtained output \( y_i \) to all other units.
8. Test the network for convergence.

### Example Problem

Consider creating a Discrete Hopfield Network with the bipolar representation of the input vector as \( [1, 1, 1, -1] \) or \( [1, 1, 1, 0] \) stored in the network. Test the network with a missing entry in the first and second components of the stored vector (i.e., \( [0, 0, 1, 0] \)).

Given the input vector \( x = [1, 1, 1, -1] \) (bipolar), initialize the weight matrix \( w_{ij} \) accordingly.

### Continuous Hopfield Network

In contrast to discrete Hopfield networks, here the time parameter is treated as continuous. Outputs range between 0 and 1, allowing for solutions to constrained optimization and associative memory problems. Output is defined as:
\[ v_i = g(u_i) \]
where \( v_i \) is the output from the continuous Hopfield network and \( u_i \) is the internal activity of a node.

### Energy Function

Hopfield networks have an associated energy function that either diminishes or remains unchanged with each update (feedback). For continuous Hopfield networks, the energy function is:
\[ E = 0.5 \sum_{i=1}^n \sum_{j=1}^n w_{ij} v_i v_j + \sum_{i=1}^n \theta_i v_i \]

To determine convergence to a stable configuration, check if the energy function reaches its minimum:
\[ \frac{dE}{dt} \leq 0 \]

The network converges if each neuron's activity over time satisfies the differential equation:
\[ \frac{du_i}{dt} = -u_i / \tau + \sum_{j=1}^n w_{ij} v_j + \theta_i \]

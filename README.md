# Hopfield Neural Network

**Last Updated:** 13 Mar, 2024

Hopfield Neural Networks, invented by Dr. John J. Hopfield, consist of one layer of ‘n’ fully connected recurrent neurons. They are used primarily for auto-association and optimization tasks. The network operates using a converging interactive process and generates distinct responses compared to traditional neural networks.

## Discrete Hopfield Network

It is a fully interconnected neural network where each unit is connected to every other unit. It operates in a discrete manner, providing finite distinct outputs, typically binary (0/1) or bipolar (-1/1).

### Structure & Architecture of Hopfield Network

- Each neuron has an inverting and non-inverting output.
- Being fully connected, the output of each neuron serves as input to all other neurons except itself.

### Discrete Hopfield Network Architecture

![Discrete Hopfield Network Architecture](path_to_image)

- [ x1 , x2 , ... , xn ] -> Input to the n given neurons.
- [ y1 , y2 , ... , yn ] -> Output obtained from the n given neurons
- Wij -> weight associated with the connection between the ith and the jth neuron.

### Training Algorithm

For storing a set of input patterns S(p) [p = 1 to P], where S(p) = S1(p) … Si(p) … Sn(p), the weight matrix is given by:

- For binary patterns:
\[ w_{ij} = \sum_{p=1}^{P} [2s_i(p) - 1][2s_j(p) - 1] \quad \text{(where } w_{ij} = w_{ji} \text{ and } i \neq j \text{)} \]

- For bipolar patterns:
\[ w_{ij} = \sum_{p=1}^{P} [s_i(p) s_j(p)] \quad \text{(where } w_{ij} = 0 \text{ for all } i = j \text{)} \]

Steps Involved in the training of a Hopfield Network:
1. Initialize weights (wij) to store patterns (using training algorithm).
2. For each input vector \( y_i \), perform steps 3-7:
   - Set initial activators of the network equal to the external input vector \( x \):
     \( y_i = x_i \) (for \( i = 1 \) to \( n \))
   - Calculate the total input of the network \( y_{in} \):
     \( y_{in, i} = x_i + \sum_j [y_j w_{ji}] \)
   - Apply activation over the total input to calculate the output:
     \[
     y_i = \begin{cases} 
     1 & \text{if } y_{in} > \theta_i \\
     y_i & \text{if } y_{in} = \theta_i \\
     0 & \text{if } y_{in} < \theta_i 
     \end{cases}
     \]
     (where \( \theta_i \) is normally 0)
   - Update activation vectors by feeding back the obtained output \( y_i \) to all other units.
3. Test the network for convergence.

### Example Problem

Consider creating a Discrete Hopfield Network with the bipolar representation of the input vector as [1, 1, 1, -1] or [1, 1, 1, 0] (in case of binary representation) stored in the network. Test the Hopfield network with missing entries in the first and second components of the stored vector (i.e., [0, 0, 1, 0]).

Given the input vector \( x = [1, 1, 1, -1] \) (bipolar), initialize the weight matrix \( w_{ij} \) as:

\[ 
w_{ij} = \sum [s^T(p) t(p)] = [111-1][111-1] = \begin{bmatrix}
1 & 1 & 1 & -1 \\
1 & 1 & 1 & -1 \\
1 & 1 & 1 & -1 \\
-1 & -1 & -1 & 1
\end{bmatrix}
\]

and weight matrix with no self-connection is:

\[ 
w_{ij} = \begin{bmatrix}
0 & 1 & 1 & -1 \\
1 & 0 & 1 & -1 \\
1 & 1 & 0 & -1 \\
-1 & -1 & -1 & 0
\end{bmatrix}
\]

As per the question, input vector \( x = [0, 0, 1, 0] \) (binary). Let \( y = x = [0, 0, 1, 0] \). Choose unit \( y_i \) (order doesn’t matter) for updating its activation and take the \( i \)th column of the weight matrix for calculation.

- Perform activation and feedback for all \( y_i \) values to check for convergence.

## Continuous Hopfield Network

In contrast to discrete Hopfield networks, here the time parameter is treated as continuous. Outputs range between 0 and 1, solving constrained optimization and associative memory problems.

### Energy Function

Hopfield networks have an energy function:
\[ E = 0.5 \sum_{i=1}^n \sum_{j=1}^n w_{ij} v_i v_j + \sum_{i=1}^n \theta_i v_i \]

For continuous Hopfield networks, to determine convergence:
\[ \frac{dE}{dt} \leq 0 \]

The network converges if:
\[ \frac{du_i}{dt} = -u_i / \tau + \sum_{j=1}^n w_{ij} v_j + \theta_i \]

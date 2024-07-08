# Hopfield Neural Network

- The Hopfield Neural Networks, invented by Dr. John J. Hopfield in 1980s, consist of one layer of ‘n’ fully connected recurrent neurons. 
- They are generally used in performing auto-association and optimization tasks. 
- They operate through a converging interactive process and generate different responses compared to traditional neural networks.

## Applications
- Pattern Recognition: Recognizes and recalls stored patterns from noisy inputs.
- Associative Memory: Stores and retrieves data like human memory.
- Optimization Problems: Solves complex combinatorial problems such as the traveling salesman problem.
- Error Correction: Corrects distorted data by converging to stored patterns.
- Neural Modeling: Models cognitive functions and neural processes.
- Image Reconstruction: Reconstructs images from incomplete or corrupted data.
- Content-Addressable Storage: Efficiently retrieves stored information based on partial data.
- Signal Processing: Enhances and retrieves original signals from noisy data.

##Types
-Discrete Hopfield Network
-Continuous Hoplified Network

## Discrete Hopfield Network

A Discrete Hopfield Network is a fully interconnected neural network where each unit is connected to every other unit. It behaves in a discrete manner, giving finite distinct outputs, generally of two types:

- **Binary (0/1)**
- **Bipolar (-1/1)**

The weights associated with this network are symmetric and have the following properties:

1. \( w_{ij} = w_{ji} \)
2. \( w_{ii} = 0 \)

### Structure & Architecture of Hopfield Network

- Each neuron has an inverting and a non-inverting output.
- Being fully connected, the output of each neuron is an input to all other neurons but not to itself.
- The below figure shows a sample representation of a Discrete Hopfield Neural Network architecture having the following elements.
  <image src="hoplified.webp" alt="Image description">


### Discrete Hopfield Network Architecture

- \( [x_1, x_2, \ldots, x_n] \) -> Input to the \( n \) given neurons.
- \( [y_1, y_2, \ldots, y_n] \) -> Output obtained from the \( n \) given neurons.
- \( w_{ij} \) -> Weight associated with the connection between the \( i \)-th and the \( j \)-th neuron.
We calculate weights in Hopfield networks to store and retrieve patterns by determining the associations between neurons.

### Training Algorithm

For storing a set of input patterns \( S(p) \) [\( p = 1 \) to \( P \)], where \( S(p) = S_1(p), \ldots, S_i(p), \ldots, S_n(p) \), the weight matrix is given by:

- **For binary patterns:**
  \[
  w_{ij} = \sum_{p=1}^{P} [2s_i(p) - 1][2s_j(p) - 1] \quad \text{(for all \( i \neq j \))}
  \]

- **For bipolar patterns:**
  \[
  w_{ij} = \sum_{p=1}^{P} s_i(p) s_j(p) \quad \text{(where \( w_{ii} = 0 \) for all \( i = j \))}
  \]

  where:
    p represents the index of the training patterns.
    P is the total number of training patterns.

    si​(p) is the state (either 0 or 1) of the ii-th neuron in the pp-th training pattern.

### Steps in Training a Hopfield Network

1. **Initialize weights** (\( w_{ij} \)) to store patterns (using the training algorithm).
2. For each input vector \( y_i \), perform steps 3-7.
3. Set the initial activations of the network equal to the external input vector \( x \):
   \[
   y_i = x_i \quad \text{(for \( i = 1 \) to \( n \))}
   \]
4. For each vector \( y_i \), perform steps 5-7.
5. Calculate the total input of the network \( y_{in} \) using the equation:
   \[
   y_{in_i} = x_i + \sum_{j} [y_j w_{ji}]
   \]
6. Apply activation over the total input to calculate the output:
   \[
   y_i = 
   \begin{cases} 
   1 & \text{if } y_{in} > \theta_i \\
   y_i & \text{if } y_{in} = \theta_i \\
   0 & \text{if } y_{in} < \theta_i 
   \end{cases}
   \]
   (where \( \theta_i \) is normally taken as 0).
7. Feedback the obtained output \( y_i \) to all other units, thus updating the activation vectors.
8. Test the network for convergence.

### Example Problem

Consider the following problem: We are required to create a Discrete Hopfield Network with the bipolar representation of the input vector as \([1, 1, 1, -1]\) or \([1, 1, 1, 0]\) (in the case of binary representation) stored in the network. Test the Hopfield network with missing entries in the first and second components of the stored vector \([0, 0, 1, 0]\).

Given the input vector \( x = [1, 1, 1, -1] \) (bipolar), initialize the weight matrix (\( w_{ij} \)) as:

\[
w_{ij} = \sum [s^T(p) t(p)] = \begin{bmatrix} 1 & 1 & 1 & -1 \end{bmatrix}^T \begin{bmatrix} 1 & 1 & 1 & -1 \end{bmatrix} = 
\begin{bmatrix} 
0 & 1 & 1 & -1 \\ 
1 & 0 & 1 & -1 \\ 
1 & 1 & 0 & -1 \\ 
-1 & -1 & -1 & 0 
\end{bmatrix}
\]

Given the input vector \( x \) with missing entries, \( x = [0, 0, 1, 0] \), make \( y_i = x = [0, 0, 1, 0] \). For each unit \( y_i \), update its activation as follows:

1. \( y_{in_1} = x_1 + \sum_{j=1}^{4} [y_j w_{j1}] = 0 + [0, 0, 1, 0] \cdot [0, 1, 1, -1] = 1 \)
   - Applying activation: \( y_{in_1} > 0 \Rightarrow y_1 = 1 \)
   - Feedback: \( y = [1, 0, 1, 0] \)
   - No convergence yet.

2. \( y_{in_3} = x_3 + \sum_{j=1}^{4} [y_j w_{j3}] = 1 + [1, 0, 1, 0] \cdot [1, 1, 0, -1] = 2 \)
   - Applying activation: \( y_{in_3} > 0 \Rightarrow y_3 = 1 \)
   - Feedback: \( y = [1, 0, 1, 0] \)
   - No convergence yet.

3. \( y_{in_4} = x_4 + \sum_{j=1}^{4} [y_j w_{j4}] = 0 + [1, 0, 1, 0] \cdot [-1, -1, -1, 0] = -2 \)
   - Applying activation: \( y_{in_4} < 0 \Rightarrow y_4 = 0 \)
   - Feedback: \( y = [1, 0, 1, 0] \)
   - No convergence yet.

4. \( y_{in_2} = x_2 + \sum_{j=1}^{4} [y_j w_{j2}] = 0 + [1, 0, 1, 0] \cdot [1, 0, 1, -1] = 2 \)
   - Applying activation: \( y_{in_2} > 0 \Rightarrow y_2 = 1 \)
   - Feedback: \( y = [1, 1, 1, 0] \)
   - Convergence achieved with vector \( x \).

## Continuous Hopfield Network

Unlike discrete Hopfield networks, here the time parameter is treated as a continuous variable. Instead of getting binary/bipolar outputs, we can obtain values that lie between 0 and 1. It can be used to solve constrained optimization and associative memory problems. The output is defined as:

\[
v_i = g(u_i)
\]

where:
- \( v_i \) = output from the continuous Hopfield network
- \( u_i \) = internal activity of a node in the continuous Hopfield network.

### Energy Function

The Hopfield networks have an energy function associated with them. It either diminishes or remains unchanged on update (feedback) after every iteration. The energy function for a continuous Hopfield network is defined as:

\[
E = 0.5 \sum_{i=1}^{n} \sum_{j=1}^{n} w_{ij} v_i v_j + \sum_{i=1}^{n} \theta_i v_i
\]

To determine if the network will converge to a stable configuration, we see if the energy function reaches its minimum by:

\[
\frac{dE}{dt} \leq 0
\]

The network is bound to converge if the activity of each neuron with respect to time is given by the following differential equation:

\[
\frac{du_i}{dt} = -\frac{u_i}{\tau} + \sum_{j=1}^{n} w_{ij} v_j + \theta_i
\]

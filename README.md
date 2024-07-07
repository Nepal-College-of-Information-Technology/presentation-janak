# presentation-janak
presentation-janak created by GitHub Classroom
# Hopfield Neural Network
*Last Updated: 13 Mar, 2024*

The Hopfield Neural Network, invented by Dr. John J. Hopfield, consists of one layer of `n` fully connected recurrent neurons. It is generally used in performing auto-association and optimization tasks. It operates using a converging interactive process and generates a different response than standard neural networks.

## Discrete Hopfield Network

It is a fully interconnected neural network where each unit is connected to every other unit. It behaves in a discrete manner, i.e., it gives finite distinct output, generally of two types:

- **Binary (0/1)**
- **Bipolar (-1/1)**

The weights associated with this network are symmetric and have the following properties:
1. `w_ij = w_ji`
2. `w_ii = 0`

### Structure & Architecture of Hopfield Network

- Each neuron has an inverting and a non-inverting output.
- Being fully connected, the output of each neuron is an input to all other neurons but not to itself.

### Discrete Hopfield Network Architecture

[ x1, x2, ..., xn ] -> Input to the n given neurons
[ y1, y2, ..., yn ] -> Output obtained from the n given neurons
W_ij -> Weight associated with the connection between the ith and the jth neuron



## Training Algorithm

For storing a set of input patterns `S(p)` [p = 1 to P], where `S(p) = S1(p) … Si(p) … Sn(p)`, the weight matrix is given by:

### For binary patterns:
\[ w_{ij} = \sum_{p=1}^P [2s_i(p) - 1][2s_j(p) - 1] \] 
(for all \( i \neq j \))

### For bipolar patterns:
\[ w_{ij} = \sum_{p=1}^P [s_i(p) s_j(p)] \] 
(where \( w_{ij} = 0 \) for all \( i = j \))

(i.e., weights here have no self-connection)

### Steps Involved in Training a Hopfield Network

1. Initialize weights \( w_{ij} \) to store patterns (using the training algorithm).
2. For each input vector \( y_i \), perform steps 3-7.
3. Make the initial activators of the network equal to the external input vector \( x \).

\[ y_i = x_i: \text{(for i = 1 to n)} \]

4. For each vector \( y_i \), perform steps 5-7.
5. Calculate the total input of the network \( y_{in} \) using the equation given below:

\[ y_{in_i} = x_i + \sum_j [y_j w_{ji}] \]

6. Apply activation over the total input to calculate the output as per the equation given below:

\[ y_i = \begin{cases} 
1 & \text{if } y_{in} > \theta_i \\
y_i & \text{if } y_{in} = \theta_i \\
0 & \text{if } y_{in} < \theta_i 
\end{cases} \]

(where \( \theta_i \) (threshold) is normally taken as 0)

7. Now feedback the obtained output \( y_i \) to all other units. Thus, the activation vectors are updated.
8. Test the network for convergence.

## Example Problem

We are required to create a Discrete Hopfield Network with the bipolar representation of the input vector as [1 1 1 -1] or [1 1 1 0] (in the case of binary representation) stored in the network. Test the Hopfield network with missing entries in the first and second components of the stored vector (i.e., [0 0 1 0]).

Given the input vector, \( x = [1 1 1 -1] \) (bipolar) and we initialize the weight matrix \( w_{ij} \) as:

\[ w_{ij} = \sum [s^T(p)t(p)] = [1 1 1 -1][1 1 1 -1] = \begin{bmatrix} 1 & 1 & 1 & -1 \\ 1 & 1 & 1 & -1 \\ 1 & 1 & 1 & -1 \\ -1 & -1 & -1 & 1 \end{bmatrix} \]

and weight matrix with no self-connection is:

\[ w_{ij} = \begin{bmatrix} 0 & 1 & 1 & -1 \\ 1 & 0 & 1 & -1 \\ 1 & 1 & 0 & -1 \\ -1 & -1 & -1 & 0 \end{bmatrix} \]

As per the question, input vector \( x \) with missing entries, \( x = [0 0 1 0] \) ([x1 x2 x3 x4]) (binary). Make \( y_i = x = [0 0 1 0] \) ([y1 y2 y3 y4]). Choosing unit \( y_i \) (order doesn’t matter) for updating its activation. Take the ith column of the weight matrix for calculation.

(we will do the next steps for all values of \( y_i \) and check if there is convergence or not)

\[ y_{in1} = x1 + \sum_{j=1}^4 [y_j w_{j1}] = 0 + [0 0 1 0][0 1 1 -1] = 0 + 1 = 1 \]
Applying activation, \( y_{in1} > 0 \) ⟹ \( y_1 = 1 \)
giving feedback to other units, we get \( y = [1 0 1 0] \)
which is not equal to input vector \( x = [1 1 1 0] \)
Hence, no convergence.

Now for next unit, we will take updated value via feedback. (i.e., \( y = [1 0 1 0] \))

\[ y_{in3} = x3 + \sum_{j=1}^4 [y_j w_{j3}] = 1 + [1 0 1 0][1 1 0 -1] = 1 + 1 = 2 \]
Applying activation, \( y_{in3} > 0 \) ⟹ \( y_3 = 1 \)
giving feedback to other units, we get \( y = [1 0 1 0] \)
which is not equal to input vector \( x = [1 1 1 0] \)
Hence, no convergence.

Now for next unit, we will take updated value via feedback. (i.e., \( y = [1 0 1 0] \))

\[ y_{in4} = x4 + \sum_{j=1}^4 [y_j w_{j4}] = 0 + [1 0 1 0][-1 -1 -1 0] = 0 + (-1) + (-1) = -2 \]
Applying activation, \( y_{in4} < 0 \) ⟹ \( y_4 = 0 \)
giving feedback to other units, we get \( y = [1 0 1 0] \)
which is not equal to input vector \( x = [1 1 1 0] \)
Hence, no convergence.

Now for next unit, we will take updated value via feedback. (i.e., \( y = [1 0 1 0] \))

\[ y_{in2} = x2 + \sum_{j=1}^4 [y_j w_{j2}] = 0 + [1 0 1 0][1 0 1 -1] = 0 + 1 + 1 = 2 \]
Applying activation, \( y_{in2} > 0 \) ⟹ \( y_2 = 1 \)
giving feedback to other units, we get \( y = [1 1 1 0] \)
which is equal to input vector \( x = [1 1 1 0] \)
Hence, convergence with vector \( x \).

## Continuous Hopfield Network

Unlike the discrete Hopfield networks, here the time parameter is treated as a continuous variable. So, instead of getting binary/bipolar outputs, we can obtain values that lie between 0 and 1. It can be used to solve constrained optimization and associative memory problems. The output is defined as:

\[ v_i = g(u_i) \]

where,
- \( v_i \) = output from the continuous Hopfield network
- \( u_i \) = internal activity of a node in the continuous Hopfield network.

### Energy Function

The Hopfield networks have an energy function associated with them. It either diminishes or remains unchanged on update (feedback) after every iteration. The energy function for a continuous Hopfield network is defined as:

\[ E = 0.5 \sum_{i=1}^n \sum_{j=1}^n w_{ij} v_i v_j + \sum_{i=1}^n \theta_i v_i \]

To determine if the network will converge to a stable configuration, we see if the energy function reaches its minimum by:

\[ \frac{dE}{dt} \leq 

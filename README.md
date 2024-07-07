# presentation-janak
presentation-janak created by GitHub Classroom
# Hopfield Neural Network
*Last Updated: 13 Mar, 2024*

The Hopfield Neural Network, invented by Dr. John J. Hopfield, consists of one layer of `n` fully connected recurrent neurons. It is generally used in performing auto-association and optimization tasks. It operates using a converging interactive process and generates a different response than standard neural networks.

## Discrete Hopfield Network

It is a fully interconnected neural network where each unit is connected to every other unit. It behaves in a discrete manner, i.e., it gives finite distinct output, generally of two types:

- **Binary (0/1)**
- **Bipolar (-1/1)*z

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

# Training Algorithm

For storing a set of input patterns \( S(p) \) [p = 1 to P], where \( S(p) = S<sub>1</sub>(p) \ldots S<sub>i</sub>(p) \ldots S<sub>n</sub>(p) \), the weight matrix is given by:

### For Binary Patterns

\[ w<sub>ij</sub> = \sum<sub>p=1</sub><sup>P</sup> [2s<sub>i</sub>(p) - 1][2s<sub>j</sub>(p) - 1] \quad \text{(for all } i \neq j \text{)} \]

### For Bipolar Patterns

\[ w<sub>ij</sub> = \sum<sub>p=1</sub><sup>P</sup> [s<sub>i</sub>(p)s<sub>j</sub>(p)] \quad \text{(where } w<sub>ij</sub> = 0 \text{ for all } i = j \text{)} \]

(i.e. weights here have no self-connection)

## Steps Involved in the Training of a Hopfield Network

1. Initialize weights \( ( w<sub>ij</sub> ) \) to store patterns (using training algorithm).

2. For each input vector \( y<sub>i</sub> \), perform steps 3-7.

3. Make the initial activators of the network equal to the external input vector \( x \).
\[ y<sub>i</sub> = x<sub>i</sub> \quad \text{(for } i = 1 \text{ to } n \text{)} \]

4. For each vector \( y<sub>i</sub> \), perform steps 5-7.

5. Calculate the total input of the network \( y<sub>\text{in}</sub> \) using the equation given below:
\[ y<sub>\text{in}, i</sub> = x<sub>i</sub> + \sum<sub>j</sub> [y<sub>j</sub> w<sub>ji</sub>] \]

6. Apply activation over the total input to calculate the output as per the equation given below:
\[ y<sub>i</sub> = \begin{cases} 
1 & \text{if } y<sub>\text{in}</sub> > \theta<sub>i</sub> \\
y<sub>i</sub> & \text{if } y<sub>\text{in}</sub> = \theta<sub>i</sub> \\
0 & \text{if } y<sub>\text{in}</sub> < \theta<sub>i</sub> 
\end{cases} \]
(where \( \theta<sub>i</sub> \) (threshold) is normally taken as 0)

7. Now feedback the obtained output \( y<sub>i</sub> \) to all other units. Thus, the activation vectors are updated.

8. Test the network for convergence.

## Example Problem

Consider the following problem. We are required to create a Discrete Hopfield Network with the bipolar representation of the input vector as \([1, 1, 1, -1]\) or \([1, 1, 1, 0]\) (in case of binary representation) stored in the network. Test the Hopfield network with missing entries in the first and second components of the stored vector (i.e., \([0, 0, 1, 0]\)).

Given the input vector, \( x = [1, 1, 1, -1] \) (bipolar), we initialize the weight matrix \( w<sub>ij</sub> \) as:

\[ 
w<sub>ij</sub> = \sum [s<sup>T</sup>(p) t(p)] = \begin{bmatrix} 1 & 1 & 1 & -1 \end{bmatrix} \begin{bmatrix} 1 \\ 1 \\ 1 \\ -1 \end{bmatrix} = \begin{bmatrix} 1 & 1 & 1 & -1 \\ 1 & 1 & 1 & -1 \\ 1 & 1 & 1 & -1 \\ -1 & -1 & -1 & 1 \end{bmatrix} 
\]

and the weight matrix with no self-connection is:

\[ 
w<sub>ij</sub> = \begin{bmatrix} 0 & 1 & 1 & -1 \\ 1 & 0 & 1 & -1 \\ 1 & 1 & 0 & -1 \\ -1 & -1 & -1 & 0 \end{bmatrix} 
\]

As per the question, input vector \( x \) with missing entries, \( x = [0, 0, 1, 0] \) (\([ x<sub>1</sub>, x<sub>2</sub>, x<sub>3</sub>, x<sub>4</sub> ]\)) (binary). Make \( y<sub>i</sub> = x = [0, 0, 1, 0] \) (\([ y<sub>1</sub>, y<sub>2</sub>, y<sub>3</sub>, y<sub>4</sub> ]\)). Choosing unit \( y<sub>i</sub> \) (order doesn’t matter) for updating its activation. Take the \( i \)-th column of the weight matrix for calculation.

(We will do the next steps for all values of \( y<sub>i</sub> \) and check if there is convergence or not)

\[ 
y<sub>\text{in}, 1</sub> = x<sub>1</sub> + \sum<sub>j=1</sub><sup>4</sup> [y<sub>j</sub> w<sub>j1</sub>] = 0 + \begin{bmatrix} 0 \\ 0 \\ 1 \\ 0 \end{bmatrix} \begin{bmatrix} 0 \\ 1 \\ 1 \\ -1 \end{bmatrix} = 0 + 1 = 1 
\]
Applying activation, \( y<sub>\text{in}, 1</sub> > 0 \implies y<sub>1</sub> = 1 \)

Giving feedback to other units, we get \( y = [1, 0, 1, 0] \) which is not equal to input vector \( x = [1, 1, 1, 0] \). Hence, no convergence.

Now for the next unit, we will take the updated value via feedback. (i.e., \( y = [1, 0, 1, 0] \))

\[ 
y<sub>\text{in}, 3</sub> = x<sub>3</sub> + \sum<sub>j=1</sub><sup>4</sup> [y<sub>j</sub> w<sub>j3</sub>] = 1 + \begin{bmatrix} 1 \\ 0 \\ 1 \\ 0 \end{bmatrix} \begin{bmatrix} 1 \\ 1 \\ 0 \\ -1 \end{bmatrix} = 1 + 1 = 2 
\]
Applying activation, \( y<sub>\text{in}, 3</sub> > 0 \implies y<sub>3</sub> = 1 \)

Giving feedback to other units, we get \( y = [1, 0, 1, 0] \) which is not equal to input vector \( x = [1, 1, 1, 0] \). Hence, no convergence.

Now for the next unit, we will take the updated value via feedback. (i.e., \( y = [1, 0, 1, 0] \))

\[ 
y<sub>\text{in}, 4</sub> = x<sub>4</sub> + \sum<sub>j=1</sub><sup>4</sup> [y<sub>j</sub> w<sub>j4</sub>] = 0 + \begin{bmatrix} 1 \\ 0 \\ 1 \\ 0 \end{bmatrix} \begin{bmatrix} -1 \\ -1 \\ -1 \\ 0 \end{bmatrix} = 0 + (-1) + (-1) = -2 
\]
Applying activation, \( y<sub>\text{in}, 4</sub> < 0 \implies y<sub>4</sub> = 0 \)

Giving feedback to other units, we get \( y = [1, 0, 1, 0] \) which is not equal to input vector \( x = [1, 1, 1, 0] \). Hence, no convergence.

Now for the next unit, we will take the updated value via feedback. (i.e., \(


\[ E = 0.5 \sum_{i=1}^n \sum_{j=1}^n w_{ij} v_i v_j + \sum_{i=1}^n \theta_i v_i

`a_ij`

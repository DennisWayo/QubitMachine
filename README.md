# QubitMachine
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Classiq IDE](https://img.shields.io/badge/Classiq-IDE-red.svg)](https://github.com/DennisWayo/QubitMachine)
[![QC](https://img.shields.io/badge/QuantumComputing-QML-blue.svg)](https://github.com/DennisWayo/QubitMachine)
[![algo](https://img.shields.io/badge/Algorithm-VQLS-blue.svg)](https://github.com/DennisWayo/QubitMachine)


Welcome! to our **Hackathon Quantum Machine Learning Track Challenge** Provided by QPoland Global Quantum Hackathon- October 2024

## Background

Variational quantum linear solvers (VQLS) represent a significant advancement in the field of quantum computing, particularly for solving linear systems of equations, which are critical across various scientific and industrial domains, such as machine learning, optimization, and computational physics. Classical methods for solving such problems can be inefficient and computationally expensive, especially when dealing with large-scale systems. Quantum algorithms, like the Variational Quantum Eigensolver (VQE) and the Harrow-Hassidim-Lloyd (HHL) algorithm, have demonstrated the potential to outperform classical counterparts in certain scenarios, but they also face limitations in terms of circuit depth and hardware noise.

The VQLS leverages the power of quantum computing combined with variational principles to minimize the resources required for solving these problems. By employing a hybrid quantum-classical approach, the quantum computer handles the state preparation and measurement, while classical optimization algorithms are used to iteratively improve the solution. This hybrid method significantly reduces the demands on quantum hardware, making VQLS particularly suited for near-term quantum devices that are characterized by noise and limited qubit coherence times.

One of the major benefits of VQLS is its scalability. The variational approach can handle larger systems with fewer qubits by compressing the state space and approximating the solution. This makes VQLS a promising tool for applications in quantum machine learning, materials science, and other fields where solving large linear systems is essential.

Variational quantum linear solver stands out as a key development for harnessing the current generation of quantum computers, allowing for efficient and scalable solutions to linear systems that classical methods struggle to compute effectively.


## Challenge 
Quantum Machine Learning: Solving Linear Systems of Equations
- Remodel or reproduce Carlos Bravo-Prieto's Variational Quantum Linear Solver using Classiq software
[![DOI:10.22331/q-2023-11-22-1188](https://zenodo.org/badge/DOI/10.22331/q-2023-11-22-1188.svg)](https://doi.org/10.22331/q-2023-11-22-1188)

## Objectives

We aimed at developing a quantum program that computes the equation involving Pauli matrices over qubits, and satisfies the requirements: 

1. A correct cost function and quantum ansatz.
2. Execute the quantum algorithm using a state-vector simulator.
3. Output the program’s CX-gate count.

## Our Methods:
 
1. Defining the Problem and Setting up the Ansatz: We expressed the given operator (Pauli-X and Pauli-Z matrices) as part of the quantum ansatz. [![ansatz](https://img.shields.io/badge/Possible-yes-green.svg)](https://github.com/DennisWayo/QubitMachine)

- The operator: 

![wayo_check](https://latex.codecogs.com/svg.image?\bg{green}\mathbf{A}=\sum_{i=1}^{10}\hat{X}i&plus;0.1\sum{j=1}^{9}\hat{Z}j\hat{Z}{j&plus;1}&plus;\mathbb{I}) Where: 

• ![wayo2](https://latex.codecogs.com/svg.image?\bg{green}\hat{X}_i) acts on the i-th qubit. 

• ![wayo3](https://latex.codecogs.com/svg.image?\bg{green}\hat{Z}j\hat{Z}{j&plus;1}) represents interactions between consecutive qubits. 

2. Creating the Ansatz Using Classiq’s Interface: We begun by defining the quantum circuit that matches this operator, utilizing Classiq to create a Hamiltonian that includes Pauli operators. [![classiq](https://img.shields.io/badge/Possible-yes-green.svg)](https://github.com/DennisWayo/QubitMachine)

3. Define the Cost Function:
To solve the equation, ![wayo4](https://latex.codecogs.com/svg.image?\bg{green}\mathbf{A}\vec{x}=0), we tried minimizing the expectation value of ![wayo6](https://latex.codecogs.com/svg.image?\bg{green}\mathbf{A}) over a trial state ![aayo7](https://latex.codecogs.com/svg.image?\bg{green}\vec{x}). This forms the cost function of the variational quantum eigensolver (VQE). [![exe](https://img.shields.io/badge/Possible-no-red.svg)](https://github.com/DennisWayo/QubitMachine)

4. Run the Simulation: Execute the algorithm using a state-vector simulator. This was implemented to calculating the exact wavefunction which was ideal for prototyping before running on a real quantum device. [![exe](https://img.shields.io/badge/Possible-yes-green.svg)](https://github.com/DennisWayo/QubitMachine)
  
6. CX-gate Count: We ensured the solution meets the challenge’s requirements, we also computed the number of CX gates used in the quantum circuit. This was done after generating the circuit. [![cx](https://img.shields.io/badge/Possible-no-red.svg)](https://github.com/DennisWayo/QubitMachine)

## Workable Qmod Solution: 
[![qmod](https://img.shields.io/badge/QMODworks-yes-green.svg)](https://github.com/DennisWayo/QubitMachine)

In this section of our solution we demonstrate how our quantum algorithm is been developed relating it to solving the equations Ax = b using quantum circuits. This approach leverages quantum state preparation, encoding of the operator, and ultimately constructing a quantum routine to solve the system.

#### 1. apply_condition Function

```python
qfunc apply_condition(index: int, qubit: qbit) {
  if ((index % 2) == 0) {
    X(qubit); // Apply Pauli-X gate if the index is even
  }
}
```

Purpose: This function applies a Pauli-X gate conditionally on specific qubits to encode information in the state. Here, if the index of a qubit is even, it applies an X (NOT) gate, flipping the qubit’s state from |0⟩ to |1⟩ or vice versa. This conditional flipping allows the encoding of certain characteristics of b in Ax = b￼, since each qubit in the state vector represents a possible solution basis for x￼.

Relation to Ax = b: The function begins to initialize the qubits in a way that could represent components of b. This encoding is foundational, as it helps prepare the quantum state for further transformations in the solution.

#### 2. block_encoding_vqls Function

```python
qfunc block_encoding_vqls(ansatz: qfunc (), block_encoding: qfunc (), prepare_b_state: qfunc ()) {
  ansatz();
  block_encoding();
  invert {
    prepare_b_state();
  }
}
```

Purpose: The block encoding function performs the heart of a variational quantum linear solver (VQLS) by applying three core steps:

	- Ansatz: Prepares an initial state (guess) for the solution of x.
	- Block Encoding: Encodes the operator A into the quantum state. This is a pivotal step because block encoding helps represent matrix operations on a quantum circuit, crucial for executing linear transformations like those represented by A.
	- Prepare ￼b State Inverse: The inversion (or uncomputation) of the b-state preparation step essentially entangles and disentangles the solution space for correct measurement probabilities.

Relation to ￼: This function orchestrates the solution by combining the ansatz (solution guess), the operator ￼, and the known vector ￼ within a quantum routine, setting up the quantum system to find an optimal solution for x.

#### 3. ax_b Function

```python
qfunc ax_b(output x: qbit[]) {
  allocate(10, x);  // Allocate qubits
  repeat (index: x.len) {
    apply_condition(index, x[index]);
  }
}
```

Purpose: This function allocates qubits to represent the vector x￼and prepares each qubit according to the conditions specified in apply_condition. It initializes the system in a superposition that reflects potential solution states for x.

Relation to Ax = b: By using apply_condition to initialize the x qubits, this function creates a base state that will interact with the block encoding of A. This interaction will ultimately allow the quantum algorithm to test whether the chosen￼x aligns with Ax = b.

#### 4. apply_operator_a Function

```python
qfunc apply_operator_a(system_qubits: qbit[]) {
  // Apply the sum of Pauli-X gates
  repeat (i: 10) {
    X(system_qubits[i]);
  }

  // Apply the sum of ZZ interaction terms
  repeat (j: 9) {
    Z(system_qubits[j]);
    Z(system_qubits[j + 1]);
  }

  // Apply identity operation to the system
  apply_to_all(IDENTITY, system_qubits);
}
```

Purpose: This function defines the matrix A as a combination of Pauli-X and ZZ interactions:

	- Pauli-X Gates: These gates are applied across the qubits, which transforms the state to apply rotations or flips, embedding part of the operator’s structure.
 
	- ZZ Interaction Terms: The two-qubit ZZ terms encode interactions between neighboring qubits. This effectively represents interaction terms in a Hamiltonian.
 
	- Identity Operation: Applying an identity ensures no further state transformations, acting as a placeholder if needed.

Relation to Ax = b: This function constructs the operator A as a combination of quantum gates. By encoding A￼with Pauli and ZZ terms, this quantum circuit is designed to represent the matrix A acting on the solution state x￼.

#### 5. main Function

```python
qfunc main(output system_qubits: qbit[], output ancillary_qubits: qbit[]) {
  allocate(10, system_qubits);
  allocate(5, ancillary_qubits);

  // Solve Ax = b
  //ax_b(system_qubits);

  // Apply the operator A as defined in the second equation
  apply_operator_a(system_qubits);
}
```

Purpose: The main function allocates qubits for system_qubits (representing x) and ancillary_qubits. It:

	- Allocates Qubits: Prepares system_qubits and ancillary_qubits, setting up the quantum circuit’s resources.
	- Applies Operator A: The commented-out ax_b(system_qubits); would initialize the state for x, but here we focus on applying apply_operator_a, which represents the matrix A in Ax = b.

Relation to Ax = b: In the main function, apply_operator_a is executed on system_qubits, encoding A into the circuit. This lets the system evolve under A, aiming to find a state x where Ax = b. The setup completes the structure to simulate and potentially measure a solution to the equation.



## Contributors
 - Dennis Wayo
 - Sabarikirishwaran Ponnambalam
 - Meenashree Khanal
 - Bhasutkar
 - Paul Dirac

## Acknoledgement
We acknoledge the efforts of the orgaisers of QPoland Global Quantum Hackathon, especially Dr Pawel Gora for the opportunity created to showcase our ideas.
[![thank](https://img.shields.io/badge/Thank-You-gold.svg)](https://github.com/DennisWayo/QubitMachine)

## License
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

# QubitMachine
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Welcome! to our Hackathon Quantum Machine Learning Track Challenge Provided by QPoland Global Quantum Hackathon

## Background

Variational quantum linear solvers (VQLS) represent a significant advancement in the field of quantum computing, particularly for solving linear systems of equations, which are critical across various scientific and industrial domains, such as machine learning, optimization, and computational physics. Classical methods for solving such problems can be inefficient and computationally expensive, especially when dealing with large-scale systems. Quantum algorithms, like the Variational Quantum Eigensolver (VQE) and the Harrow-Hassidim-Lloyd (HHL) algorithm, have demonstrated the potential to outperform classical counterparts in certain scenarios, but they also face limitations in terms of circuit depth and hardware noise.

The VQLS leverages the power of quantum computing combined with variational principles to minimize the resources required for solving these problems. By employing a hybrid quantum-classical approach, the quantum computer handles the state preparation and measurement, while classical optimization algorithms are used to iteratively improve the solution. This hybrid method significantly reduces the demands on quantum hardware, making VQLS particularly suited for near-term quantum devices that are characterized by noise and limited qubit coherence times.

One of the major benefits of VQLS is its scalability. The variational approach can handle larger systems with fewer qubits by compressing the state space and approximating the solution. This makes VQLS a promising tool for applications in quantum machine learning, materials science, and other fields where solving large linear systems is essential.

Variational quantum linear solver stands out as a key development for harnessing the current generation of quantum computers, allowing for efficient and scalable solutions to linear systems that classical methods struggle to compute effectively.


## Challenge 
Quantum Machine Learning: Solving Linear Systems of Equations
- Remodel or reproduce Carlos Bravo-Prieto's Variational Quantum Linear Solver using Classiq software
<https://quantum-journal.org/papers/q-2023-11-22-1188/>

## Objectives

We aimed at developing a quantum program that computes the equation involving Pauli matrices over qubits, and satisfies the requirements: 

1. A correct cost function and quantum ansatz.
2. Execute the quantum algorithm using a state-vector simulator.
3. Output the program’s CX-gate count.

## Our Methods:
 
1. Defining the Problem and Setting up the Ansatz: We expressed the given operator (Pauli-X and Pauli-Z matrices) as part of the quantum ansatz.

- The operator: 

```math
\mathbf{A} = \sum_{i=1}^{10} \hat{X}i + 0.1 \sum{j=1}^{9} \hat{Z}j \hat{Z}{j+1} + \mathbb{I} 
Where: 
• \hat{X}_i acts on the i-th qubit. 
• \hat{Z}j \hat{Z}{j+1} represents interactions between consecutive qubits. 
```

```math
![wayo_check](https://latex.codecogs.com/svg.image?\mathbf{A}=\sum_{i=1}^{10}\hat{X}i&plus;0.1\sum{j=1}^{9}\hat{Z}j\hat{Z}{j&plus;1}&plus;\mathbb{I})
```
![grad_desc_url](https://latex.codecogs.com/gif.latex?w_{i&plus;1}&space;=&space;w_i&space;-&space;\epsilon&space;\cdot&space;\left.\frac{dL}{dw}\right|_{w_i})

$$\mathbf{A} = \sum_{i=1}^{10} \hat{X}i + 0.1 \sum{j=1}^{9} \hat{Z}j \hat{Z}{j+1} + \mathbb{I}$$

2. Creating the Ansatz Using Classiq’s Interface: We begun by defining the quantum circuit that matches this operator, utilizing Classiq to create a Hamiltonian that includes Pauli operators. 
3. Define the Cost Function:
To solve the equation, 

```math
\mathbf{A} \vec{x} = 0, 
```
we minimized the expectation value of $$\mathbf{A}$$ over a trial state $$\vec{x}$$. This forms the cost function of the variational quantum eigensolver (VQE).

4. Run the Simulation:Execute the algorithm using a state-vector simulator. This was implemented to calculating the exact wavefunction which was ideal for prototyping before running on a real quantum device.
5. CX-gate Count: We ensured the solution meets the challenge’s requirements, we also computed the number of CX gates used in the quantum circuit. This was done after generating the circuit.

## Solutions: 

Simulate our solutions by 
- downloading  our qubitmachine_model.py file, 
- open Classiq interface online, and 
- upload the model, synthesize and execute. 

add video here

## Bonus: VQLS Model in QML
Our team took the challenge further by incorporating the VQLS code into quantum machine learning to simulate a real dataset. 

## Contributors
 - Dennis Wayo
 - Sabarikirishwaran Ponnambalam
 - Meenashree Khanal
 - Bhasutkar
 - Paul Dirac

## Acknoledgement
xxxx

## License
MIT
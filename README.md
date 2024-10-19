# QubitMachine
Welcome! to our Hackathon Challenge provided by QPoland Global Quantum Hackathon

> Problem Background

Solving a linear system that grows in size becomes more difficult. In reference to Carlos Bravo-Prietos' Variational Quantum Linear Algorithm Solver


> Challenge Objectives

Here’s a step-by-step guide to submitting a solution to your challenge using Classiq, involving Pauli matrices and quantum program creation: Objective:

• Write a quantum program that computes the equation involving Pauli matrices over qubits, and satisfies the requirements: 
1. A correct cost function and quantum ansatz.
2. Execute the quantum algorithm using a state-vector simulator.
3. Output the program’s CX-gate count.

> Our Methods:
 
1. Defining the Problem and Setting up the Ansatz: We expressed the given operator (Pauli-X and Pauli-Z matrices) as part of the quantum ansatz.

- The operator: 
\mathbf{A} = \sum_{i=1}^{10} \hat{X}i + 0.1 \sum{j=1}^{9} \hat{Z}j \hat{Z}{j+1} + \mathbb{I} Where: • \hat{X}_i acts on the i-th qubit. • \hat{Z}j \hat{Z}{j+1} represents interactions between consecutive qubits. 

2. Creating the Ansatz Using Classiq’s Interface: We begun by defining the quantum circuit that matches this operator, utilizing Classiq to create a Hamiltonian that includes Pauli operators. 

3. Define the Cost Function:
To solve the equation \mathbf{A} \vec{x} = 0, we minimized the expectation value of \mathbf{A} over a trial state \vec{x}. This forms the cost function of the variational quantum eigensolver (VQE).

4. Run the Simulation:
Execute the algorithm using a state-vector simulator. This is useful for calculating the exact wavefunction and is ideal for prototyping before running on a real quantum device.

5. CX-gate Count: To ensure the solution meets the challenge’s requirements, we must also compute the number of CX gates used in the quantum circuit. This can be done after generating the circuit.

> Solutions: download our qubitmachine_model.py file, open Classiq interface online, and upload the model, synthesize and execute. 



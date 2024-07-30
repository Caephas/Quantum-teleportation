# Quantum Teleportation and Gate Teleportation with Qiskit

This project demonstrates the implementation of both quantum state teleportation and gate teleportation using Qiskit. Quantum teleportation is a process by which the state of a qubit (Alice's qubit) is transmitted to another qubit (Bob's qubit) using entanglement and classical communication. Gate teleportation allows a quantum gate operation to be transferred from one qubit to another, also using entanglement and classical communication.

## Requirements

- Python 3.x
- Qiskit
- Matplotlib

## Installation

To run this project, you need to install Qiskit and Matplotlib. You can install these using pip:

```bash
pip install qiskit matplotlib
```

## Steps in the Code

### 1. Initialize the Circuit

We start by initializing a quantum circuit with 3 qubits and 3 classical bits.

### 2. Entangle Qubits

Next, we create an entangled state between qubit 1 (Alice's entangled qubit) and qubit 2 (Bob's qubit) using a Hadamard gate and a CNOT gate.

### 3. Prepare Alice's Qubit

Prepare Alice's qubit (qubit 0) in an initial state |ψ⟩. Here, we use a Hadamard gate to create a superposition state.

### 4. Perform Bell Measurement

Perform a Bell measurement on qubit 0 and qubit 1 (Alice's qubits) to entangle them and prepare for teleportation.

### 5. Measure and Communicate

Measure qubits 0 and 1, and store the results in classical bits 0 and 1. This step represents the classical communication part of the teleportation protocol.

### 6. Apply Corrections to Bob's Qubit

Use the classical bits to apply the necessary corrections to qubit 2 (Bob's qubit). Depending on the measurement results, apply the appropriate gates.

### 7. Measure Bob's Qubit

Finally, measure Bob's qubit to verify the teleportation.

### 8. Execute the Circuit

Simulate the circuit using Qiskit's AerSimulator and print the results.

### 9. Visualize the Results

Plot the histogram of the results to visualize the distribution of the measured states.

### 10. Analyze Measurement Results

Separate the counts for each qubit and plot them individually for better visualization.

## Gate Teleportation

### Concept

Gate teleportation involves transferring the action of a quantum gate from one qubit to another, using entanglement and classical communication. This technique ensures that the gate operation can be applied indirectly.

### Steps

1. **Initialize the Circuit**: Initialize a quantum circuit with 3 qubits and 2 classical bits.
2. **Create Entangled Pair**: Create an entangled pair between qubit 1 and qubit 2.
3. **Apply Gate to Qubit**: Apply a quantum gate (e.g., X gate) to qubit 0.
4. **Perform Bell Measurements**: Perform Bell measurements on qubits 0 and 1.
5. **Measure and Communicate**: Measure qubits 0 and 1, and store the results in classical bits 0 and 1.
6. **Apply Corrections**: Apply corrections to qubit 2 based on the measurement results.

## Conclusion

This project demonstrates the fundamental concepts of quantum teleportation and gate teleportation using Qiskit. By entangling qubits, performing Bell measurements, and applying conditional operations based on classical communication, we can teleport the state of one qubit to another or transfer a quantum gate operation. The visualization of the measurement results confirms the success of these teleportation protocols.

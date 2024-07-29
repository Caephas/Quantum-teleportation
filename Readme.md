# Quantum Teleportation with Qiskit

This project demonstrates the implementation of quantum teleportation using Qiskit. Quantum teleportation is a process by which the state of a qubit (Alice's qubit) is transmitted to another qubit (Bob's qubit) using entanglement and classical communication.

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

```python
from qiskit import QuantumCircuit

qc = QuantumCircuit(3, 3)
qc.draw('mpl')
```

### 2. Entangle Qubits

Next, we create an entangled state between qubit 1 (Alice's entangled qubit) and qubit 2 (Bob's qubit) using a Hadamard gate and a CNOT gate.

```python
# Step 1: Entangle
qc.h(1)       # Create superposition on qubit 1
qc.cx(1, 2)   # Entangle qubit 1 with qubit 2
qc.draw('mpl')
```

### 3. Prepare Alice's Qubit

Prepare Alice's qubit (qubit 0) in an initial state |ψ⟩. Here, we use a Hadamard gate to create a superposition state.

```python
# Prepare Alice's qubit (qubit 0) in an initial state
qc.h(0)
qc.draw('mpl')
```

### 4. Perform Bell Measurement

Perform a Bell measurement on qubit 0 and qubit 1 (Alice's qubits) to entangle them and prepare for teleportation.

```python
# Step 2: Encode
qc.cx(0, 1)
qc.h(0)
qc.draw('mpl')
```

### 5. Measure and Communicate

Measure qubits 0 and 1, and store the results in classical bits 0 and 1. This step represents the classical communication part of the teleportation protocol.

```python
# Step 3: Communicate
qc.measure([0, 1], [0, 1])
qc.draw('mpl')
```

### 6. Apply Corrections to Bob's Qubit

Use the classical bits to apply the necessary corrections to qubit 2 (Bob's qubit). Depending on the measurement results, apply the appropriate gates.

```python
# Step 4: Decode
qc.cx(1, 2)
qc.cz(0, 2)
qc.draw('mpl')
```

### 7. Measure Bob's Qubit

Finally, measure Bob's qubit to verify the teleportation.

```python
qc.measure(2, 2)
qc.draw('mpl')
```

### 8. Execute the Circuit

Simulate the circuit using Qiskit's AerSimulator and print the results.

```python
from qiskit_aer import AerSimulator
from qiskit import transpile, execute

simulator = AerSimulator()
compiled_circuit = transpile(qc, simulator)
job = simulator.run(compiled_circuit)
result = job.result()

# Get and print the results
counts = result.get_counts(compiled_circuit)
print("\nTotal count for each state are:\n", counts)
```

### 9. Visualize the Results

Plot the histogram of the results to visualize the distribution of the measured states.

```python
from qiskit.visualization import plot_histogram
import matplotlib.pyplot as plt

plot_histogram(counts)
plt.show()
```

### 10. Analyze Measurement Results

Separate the counts for each qubit and plot them individually for better visualization.

```python
# Separate counts for each qubit
qubit_0_counts = {'0': 0, '1': 0}
qubit_1_counts = {'0': 0, '1': 0}
qubit_2_counts = {'0': 0, '1': 0}

# Sum counts based on the measurement outcomes of each qubit
for state, count in counts.items():
    qubit_2_counts[state[0]] += count
    qubit_1_counts[state[1]] += count
    qubit_0_counts[state[2]] += count

# Plotting the results
fig, ax = plt.subplots(1, 3, figsize=(18, 6))

ax[0].bar(qubit_0_counts.keys(), qubit_0_counts.values(), color='blue')
ax[0].set_title('Qubit 0')
ax[0].set_xlabel('State')
ax[0].set_ylabel('Counts')

ax[1].bar(qubit_1_counts.keys(), qubit_1_counts.values(), color='green')
ax[1].set_title('Qubit 1')
ax[1].set_xlabel('State')
ax[1].set_ylabel('Counts')

ax[2].bar(qubit_2_counts.keys(), qubit_2_counts.values(), color='red')
ax[2].set_title('Qubit 2')
ax[2].set_xlabel('State')
ax[2].set_ylabel('Counts')

plt.show()
```

## Conclusion

This project demonstrates the fundamental concepts of quantum teleportation using Qiskit. By entangling qubits, performing Bell measurements, and applying conditional operations based on classical communication, we can teleport the state of one qubit to another. The visualization of the measurement results confirms the success of the teleportation protocol.

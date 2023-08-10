# Python code to demonstrate the working of Teleportation in Qiskit
from qiskit import Aer, QuantumCircuit, transpile, assemble

# Function to create the Bell state |Φ+⟩ = (|00⟩ + |11⟩)/√2
def create_bell_pair(qc, a, b):
    qc.h(a)
    qc.cx(a, b)

# Function to apply the teleportation protocol
def teleport(qc, psi, a, b):
    qc.cx(psi, a)
    qc.h(psi)
    qc.barrier()
    qc.measure(psi, 0)
    qc.measure(a, 1)
    qc.barrier()
    qc.cx(a, b)
    qc.cz(psi, b)

# Main function to demonstrate teleportation
def main():
    # Create a quantum circuit with 3 qubits (psi, Alice's qubit, Bob's qubit)
    qc = QuantumCircuit(3, 3)

    # Prepare the state to be teleported (psi) - For simplicity, let's use |1⟩
    psi = 0
    qc.x(psi)

    # Create the Bell pair between Alice's and Bob's qubits
    create_bell_pair(qc, 1, 2)

    # Teleport the state psi to Bob's qubit
    teleport(qc, psi, 0, 1)

    # Measure the qubits and extract the result
    backend = Aer.get_backend('qasm_simulator')
    t_qc = transpile(qc, backend)
    qobj = assemble(t_qc)
    result = backend.run(qobj).result()
    counts = result.get_counts(qc)

    print("Teleportation Result:")
    print(counts)

if __name__ == "__main__":
    main()

# Interferencia-cuantica
!pip install cirq
import cirq
import numpy as np
import matplotlib.pyplot as plt

# Crear un qubit
qubit = cirq.GridQubit(0, 0)

# Construir el circuito
circuit = cirq.Circuit()

# 1. Aplicar una puerta de Hadamard para crear superposición
circuit.append(cirq.H(qubit))

# 2. Aplicar una fase condicional con una puerta Z (simula interferencia)
circuit.append(cirq.Z(qubit))

# 3. Aplicar otra puerta de Hadamard para completar la interferencia
circuit.append(cirq.H(qubit))

# 4. Medir el qubit
circuit.append(cirq.measure(qubit, key='result'))

# Simulador cuántico
simulator = cirq.Simulator()

# Ejecutar el circuito varias veces
resultados = simulator.run(circuit, repetitions=1000)

# Obtener las frecuencias de los resultados
frecuencias = resultados.histogram(key='result')

# Graficar los resultados
labels = ['0', '1']
valores = [frecuencias[0] if 0 in frecuencias else 0, frecuencias[1] if 1 in frecuencias else 0]

plt.bar(labels, valores, color=['blue', 'orange'])
plt.title("Resultados de la interferencia cuántica")
plt.xlabel("Estado medido")
plt.ylabel("Frecuencia")
plt.show()

# Mostrar el circuito
print("Circuito Cuántico:")
print(circuit)

# EJEMPLO ADICIONAL
# Crear un segundo circuito con dos qubits para demostrar entrelazamiento
qubit1 = cirq.GridQubit(1, 0)
qubit2 = cirq.GridQubit(1, 1)

# Construir el circuito
circuit_entrelazado = cirq.Circuit()

# 1. Crear superposición en el primer qubit
circuit_entrelazado.append(cirq.H(qubit1))

# 2. Entrelazar los qubits usando una puerta CNOT
circuit_entrelazado.append(cirq.CNOT(qubit1, qubit2))

# 3. Medir ambos qubits
circuit_entrelazado.append(cirq.measure(qubit1, key='result1'))
circuit_entrelazado.append(cirq.measure(qubit2, key='result2'))

# Ejecutar el segundo circuito varias veces
resultados_entrelazados = simulator.run(circuit_entrelazado, repetitions=1000)

# Obtener las frecuencias de los resultados
frecuencias_entrelazadas = resultados_entrelazados.multi_measurement_histogram(keys=['result1', 'result2'])

# Preparar los datos para graficar
labels_entrelazados = [f"{key[0]}{key[1]}" for key in frecuencias_entrelazadas.keys()]
valores_entrelazados = list(frecuencias_entrelazadas.values())

# Graficar los resultados del entrelazamiento
plt.bar(labels_entrelazados, valores_entrelazados, color=['green', 'red', 'purple', 'cyan'])
plt.title("Resultados del entrelazamiento cuántico")
plt.xlabel("Estados medidos (Qubit1Qubit2)")
plt.ylabel("Frecuencia")
plt.show()

# Mostrar el circuito entrelazado
print("Circuito Cuántico para Entrelazamiento:")
print(circuit_entrelazado)


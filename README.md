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

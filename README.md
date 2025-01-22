# Interferencia cuántica con un ejemplo adicional
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
# Crear un segundo ejemplo de interferencia cuántica
qubit_extra = cirq.GridQubit(1, 0)

# Construir el circuito
circuit_extra = cirq.Circuit()

# 1. Crear superposición inicial
circuit_extra.append(cirq.H(qubit_extra))

# 2. Aplicar una puerta de fase S (cuadrada de Z) para cambiar la fase
circuit_extra.append(cirq.S(qubit_extra))

# 3. Aplicar otra puerta Hadamard para interferencia
circuit_extra.append(cirq.H(qubit_extra))

# 4. Medir el qubit
circuit_extra.append(cirq.measure(qubit_extra, key='result_extra'))

# Ejecutar el segundo circuito varias veces
resultados_extra = simulator.run(circuit_extra, repetitions=1000)

# Obtener las frecuencias de los resultados
frecuencias_extra = resultados_extra.histogram(key='result_extra')

# Graficar los resultados
labels_extra = ['0', '1']
valores_extra = [frecuencias_extra[0] if 0 in frecuencias_extra else 0, frecuencias_extra[1] if 1 in frecuencias_extra else 0]

plt.bar(labels_extra, valores_extra, color=['purple', 'green'])
plt.title("Resultados de la interferencia cuántica (Ejemplo Adicional)")
plt.xlabel("Estado medido")
plt.ylabel("Frecuencia")
plt.show()

# Mostrar el circuito adicional
print("Circuito Cuántico Adicional:")
print(circuit_extra)


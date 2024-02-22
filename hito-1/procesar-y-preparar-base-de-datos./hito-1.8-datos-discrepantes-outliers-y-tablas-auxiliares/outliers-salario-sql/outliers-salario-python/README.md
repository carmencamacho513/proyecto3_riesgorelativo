# Outliers Salario Python

```python
df = df.dropna(subset=['ultimo_salario'])
ultimo_salario = df['ultimo_salario'].values

# Identificación de valores atípicos
Q1 = np.percentile(ultimo_salario, 25)
Q3 = np.percentile(ultimo_salario, 75)
IQR = Q3 - Q1

# Calcular los límites para identificar outliers
limite_inferior = Q1 - 1.5 * IQR
limite_superior = Q3 + 1.5 * IQR

# Identificar los outliers
outliers = (ultimo_salario < limite_inferior) | (ultimo_salario > limite_superior)

# Imprimir los resultados
print(f"Límite Inferior: {limite_inferior}")
print(f"Límite Superior: {limite_superior}")
print("Outliers:")
print(ultimo_salario[outliers])
```

Límite Inferior: -3950.0&#x20;

Límite Superior: 15650.0&#x20;

Outliers: \[18750. 18856. 16666. ... 17400. 21000. 35000.]

## Conclusiones

Como muestra el calculo el límite inferior es -3950, el límite superior es 15.650 y los outliers que dieron como resultado son los sueldos que estan por encima del límite superior 15.650 dolares.



###

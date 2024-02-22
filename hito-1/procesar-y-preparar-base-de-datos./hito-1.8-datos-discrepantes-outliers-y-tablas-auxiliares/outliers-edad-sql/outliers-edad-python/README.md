# Outliers Edad Python

```python
edad = df['edad'].values
# Identificación de valores atípicos
Q1 = np.percentile(edad, 25)
Q3 = np.percentile(edad, 75)
IQR = Q3 - Q1

# Calcular los límites para identificar outliers
limite_inferior = Q1 - 1.5 * IQR
limite_superior = Q3 + 1.5 * IQR

# Identificar los outliers
outliers = (edad < limite_inferior) | (edad > limite_superior)

# Imprimir los resultados
print(f"Límite Inferior: {limite_inferior}")
print(f"Límite Superior: {limite_superior}")
print("Outliers:")
print(edad[outliers])
```

Límite Inferior: 8.0&#x20;

Límite Superior: 96.0&#x20;

Outliers: \[101, 97, 97, 97, 97, 103, 97, 109, 97, 98] Length: 10, dtype: Int64

## Conclusiones

Como muestra el calculo el límite inferior es 8.0, el límite superior es 96 y los outliers que dieron como resultado es lo que esta por encima del límite superior o sea edades iguales o mayores a 97 años.



###

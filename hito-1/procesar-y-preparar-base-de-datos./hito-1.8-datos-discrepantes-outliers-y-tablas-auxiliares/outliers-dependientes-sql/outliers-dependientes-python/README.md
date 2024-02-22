# Outliers Dependientes Python

```python
dependientes = df['dependientes'].values

# Identificación de valores atípicos
Q1 = np.percentile(dependientes, 25)
Q3 = np.percentile(dependientes, 75)
IQR = Q3 - Q1

# Calcular los límites para identificar outliers
limite_inferior = Q1 - 1.5 * IQR
limite_superior = Q3 + 1.5 * IQR

# Identificar los outliers
outliers = (dependientes < limite_inferior) | (dependientes > limite_superior)

# Imprimir los resultados
print(f"Límite Inferior: {limite_inferior}")
print(f"Límite Superior: {limite_superior}")
print("Outliers:")
print(dependientes[outliers])
```

Límite Inferior: -3.0

&#x20;Límite Superior: 5.0&#x20;

Outliers: \[ 6, 7, 8, 6, 6, 6, 6, 6, 7, 6, 8, 6, 13, 6, 7, 7, 6, 6, 7, 6, 6, 7, 6, 6, 6, 6, 6, 10, 6, 7, 6, 6, 6, 7, 6, 6, 7, 6, 6, 7, 9, 6, 6, 6, 8, 6, 7, 8, 8, 6, 6, 6, 8, 8, 6, 6, 9, 6, 9, 6, 7] Length: 61, dtype: Int64.

## Conclusiones

Como muestra el calculo el límite inferior es -3.0, el límite superior es 5.0 y los outliers que dieron como resultado es lo que esta por encima del límite superior o sea dependientes iguales o mayores a 6.



###


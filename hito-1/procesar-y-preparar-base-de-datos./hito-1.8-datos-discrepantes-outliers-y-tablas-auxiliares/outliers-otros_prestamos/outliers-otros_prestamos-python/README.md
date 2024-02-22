# Outliers otros\_prestamos Python

```sql
df = df.dropna(subset=['otros_prestamos'])
otros_prestamos = df['otros_prestamos'].values

# Identificación de valores atípicos
Q1 = np.percentile(otros_prestamos, 25)
Q3 = np.percentile(otros_prestamos, 75)
IQR = Q3 - Q1

# Calcular los límites para identificar outliers
limite_inferior = Q1 - 1.5 * IQR
limite_superior = Q3 + 1.5 * IQR

# Identificar los outliers
outliers = (otros_prestamos < limite_inferior) | (otros_prestamos > limite_superior)

# Imprimir los resultados
print(f"Límite Inferior: {limite_inferior}")
print(f"Límite Superior: {limite_superior}")
print("Outliers:")
print(otros_prestamos[outliers])
```

Límite Inferior: -5.0&#x20;

Límite Superior: 19.0&#x20;

Outliers: \[20, 28, 24, 21, 21, 24, 31, 41, 21, 20, ... 32, 21, 24, 21, 20, 24, 39, 22, 23, 30] Length: 698, dtype: Int64

## Conclusiones

Como muestra el calculo el límite inferior es -5.0, el límite superior es 19.0 y los outliers que dieron como resultado es lo que esta por encima del límite superior o sea cantidad de otros creditos iguales o mayores a 20.



###

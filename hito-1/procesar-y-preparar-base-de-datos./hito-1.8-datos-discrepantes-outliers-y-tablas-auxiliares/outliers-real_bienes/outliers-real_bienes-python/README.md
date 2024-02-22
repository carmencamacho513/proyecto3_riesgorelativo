# Outliers real\_bienes Python

```sql
df = df.dropna(subset=['real_bienes'])
real_bienes = df['real_bienes'].values

# Identificación de valores atípicos
Q1 = np.percentile(real_bienes, 25)
Q3 = np.percentile(real_bienes, 75)
IQR = Q3 - Q1

# Calcular los límites para identificar outliers
limite_inferior = Q1 - 1.5 * IQR
limite_superior = Q3 + 1.5 * IQR

# Identificar los outliers
outliers = (real_bienes < limite_inferior) | (real_bienes > limite_superior)

# Imprimir los resultados
print(f"Límite Inferior: {limite_inferior}")
print(f"Límite Superior: {limite_superior}")
print("Outliers:")
print(real_bienes[outliers])
```

Límite Inferior: -3.0&#x20;

Límite Superior: 5.0&#x20;

Outliers: \[ 6, 7, 6, 6, 6, 25, 8, 8, 7, 7, ... 7, 8, 6, 9, 9, 6, 6, 15, 7, 8] Length: 157, dtype: Int64

## Conclusiones

Como muestra el calculo el límite inferior es -3.0, el límite superior es 5.0 y los outliers que dieron como resultado es lo que esta por encima del límite superior o sea cantidad de creditos iguales o mayores a 6.



###

##

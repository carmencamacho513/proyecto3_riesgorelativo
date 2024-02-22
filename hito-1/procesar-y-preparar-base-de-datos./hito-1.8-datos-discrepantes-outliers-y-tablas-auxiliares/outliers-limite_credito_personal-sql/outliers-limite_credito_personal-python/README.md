# Outliers limite\_credito\_personal Python

```python
limite_credito_personal = df['limite_credito_personal'].values

# Identificación de valores atípicos
Q1 = np.percentile(limite_credito_personal, 25)
Q3 = np.percentile(limite_credito_personal, 75)
IQR = Q3 - Q1

# Calcular los límites para identificar outliers
limite_inferior = Q1 - 1.5 * IQR
limite_superior = Q3 + 1.5 * IQR

# Identificar los outliers
outliers = (limite_credito_personal < limite_inferior) | (limite_credito_personal > limite_superior)

# Imprimir los resultados
print(f"Límite Inferior: {limite_inferior}")
print(f"Límite Superior: {limite_superior}")
print("Outliers:")
print(limite_credito_personal[outliers])
```

<figure><img src="../../../../../.gitbook/assets/image (63).png" alt=""><figcaption></figcaption></figure>

## Conclusiones

Como muestra el calculo el límite inferior es -0.763947, el límite superior es 1.366290486 y los outliers que dieron como resultado es lo que esta por encima del límite superior.



###

# Outliers Ratio Deuda Python

```python
ratio_deuda = df['ratio_deuda'].values

# Identificación de valores atípicos
Q1 = np.percentile(ratio_deuda, 25)
Q3 = np.percentile(ratio_deuda, 75)
IQR = Q3 - Q1

# Calcular los límites para identificar outliers
limite_inferior = Q1 - 1.5 * IQR
limite_superior = Q3 + 1.5 * IQR

# Identificar los outliers
outliers = (ratio_deuda < limite_inferior) | (ratio_deuda > limite_superior)

# Imprimir los resultados
print(f"Límite Inferior: {limite_inferior}")
print(f"Límite Superior: {limite_superior}")
print("Outliers:")
print(ratio_deuda[outliers])
```

Límite Inferior: -0.36544670199999985&#x20;

Límite Superior: 0.9922171539999999&#x20;

Outliers: \[7.34000000e+02 1.04398241e+00 1.56579678e+00 ... 1.27048634e+00 4.46000000e+03 1.31107127e+00]

## Conclusiones

Como muestra el calculo el límite inferior es -0.36544670199999985, el límite superior es 0.9922171539999999 y los outliers que dieron como resultado es lo que esta por encima del límite superior \[7.34000000e+02 1.04398241e+00 1.56579678e+00 ... 1.27048634e+00 4.46000000e+03 1.31107127e+00].



###

# Outliers mas90\_dias\_vencido Python

```python
# Eliminar filas con valores no numéricos o NaN en 'estado_mora'
df = df.dropna(subset=['mas90_dias_vencido'], how='any', axis=0)

# Convertir la columna a tipo float
df['mas90_dias_vencido'] = df['mas90_dias_vencido'].astype(float)

# Obtener la columna después de realizar cambios
mas90_dias_vencido = df['mas90_dias_vencido'].values

# Calcular Z-score
z_scores = stats.zscore(mas90_dias_vencido)

# Identificar outliers basados en un umbral de Z-score
umbral_zscore = 3
outliers_zscore = np.abs(z_scores) > umbral_zscore

# Imprimir resultados
print("Outliers basados en Z-score:")
print(mas90_dias_vencido[outliers_zscore])
```

<figure><img src="../../../../../.gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure>

## Conclusiones

Después de aplicar el método IQR y observar que los límites y el IQR eran 0, decidí complementar la identificación de outliers utilizando el Z-score.

El Z-score proporciona una medida estandarizada de la posición de un valor en relación con la media y la desviación estándar. Aunque el IQR no mostró variabilidad, el Z-score puede revelar valores que, a pesar de tener un IQR pequeño, están significativamente alejados de la media.

Como resultado nos dio datos positivos.&#x20;



###

###

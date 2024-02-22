# Outliers mas60\_89dias\_vencido Python

```python
# Eliminar filas con valores no numéricos o NaN en 'estado_mora'
df = df.dropna(subset=['mas60_89dias_vencido'], how='any', axis=0)

# Convertir la columna a tipo float
df['mas60_89dias_vencido'] = df['mas60_89dias_vencido'].astype(float)

# Obtener la columna después de realizar cambios
mas60_89dias_vencido = df['mas60_89dias_vencido'].values

# Calcular Z-score
z_scores = stats.zscore(mas60_89dias_vencido)

# Identificar outliers basados en un umbral de Z-score
umbral_zscore = 3
outliers_zscore = np.abs(z_scores) > umbral_zscore

# Imprimir resultados
print("Outliers basados en Z-score:")
print(mas60_89dias_vencido[outliers_zscore])
```

Outliers basados en Z-score: \[98. 98. 98. 98. 98. 98. 98. 98. 98. 98. 98. 98. 98. 98. 98. 98. 98. 98. 98. 98. 96. 98. 98. 98. 98. 98. 98. 98. 98. 98. 98.]

## Conclusiones

Después de aplicar el método IQR y observar que los límites y el IQR eran 0, decidí complementar la identificación de outliers utilizando el Z-score.

El Z-score proporciona una medida estandarizada de la posición de un valor en relación con la media y la desviación estándar. Aunque el IQR no mostró variabilidad, el Z-score puede revelar valores que, a pesar de tener un IQR pequeño, están significativamente alejados de la media.

Como resultado nos dio datos positivos \[98. 98. 98. 98. 98. 98. 98. 98. 98. 98. 98. 98. 98. 98. 98. 98. 98. 98. 98. 98. 96. 98. 98. 98. 98. 98. 98. 98. 98. 98. 98.]

###

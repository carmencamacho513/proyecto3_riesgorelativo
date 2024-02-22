# Histograma-Boxplot limite\_credito\_personal Python

```python
limite_credito_personal = df['limite_credito_personal'].values

# Histograma
plt.figure(figsize=(10, 5))
plt.subplot(1, 2, 1) 
plt.hist(limite_credito_personal, bins=15, color='Aqua', alpha=0.7)
plt.title('Histograma de limite_credito_personal')
plt.xlabel('limite_credito_personal')
plt.ylabel('Frecuencia')

# Boxplot
plt.subplot(1, 2, 2) 
plt.boxplot(limite_credito_personal, vert=False, widths=0.7, patch_artist=True, boxprops=dict(facecolor='DeepPink'))
plt.title('Boxplot de limite_credito_personal')
plt.xlabel('limite_credito_personal')

# Gráficos
plt.tight_layout()
plt.show()
```

<figure><img src="../../../../../.gitbook/assets/image (85).png" alt=""><figcaption></figcaption></figure>

## Conclusiones

Como aparece en el histograma podemos identificar rápidamente que está sesgada hacia la derecha (o con la cola hacia la derecha). Esto indica que la mayor parte de la concentración de datos se encuentra al comienzo de la distribución.

En la caja Boxplot se ve como la mayoría de outliers por encima del límite superior.

###

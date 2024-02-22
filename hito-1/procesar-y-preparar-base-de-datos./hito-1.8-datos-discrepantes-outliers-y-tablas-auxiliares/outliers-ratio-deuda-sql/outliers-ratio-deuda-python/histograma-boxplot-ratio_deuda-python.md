# Histograma-Boxplot ratio\_deuda Python

```python
ratio_deuda = df['ratio_deuda'].values

# Histograma
plt.figure(figsize=(10, 5))
plt.subplot(1, 2, 1) 
plt.hist(ratio_deuda, bins=15, color='MediumBlue', alpha=0.7)
plt.title('Histograma de ratio_deuda')
plt.xlabel('ratio_deuda')
plt.ylabel('Frecuencia')

# Boxplot
plt.subplot(1, 2, 2) 
plt.boxplot(ratio_deuda, vert=False, widths=0.7, patch_artist=True, boxprops=dict(facecolor='Chocolate'))
plt.title('Boxplot de ratio_deuda')
plt.xlabel('ratio_deuda')

# Gráficos
plt.tight_layout()
plt.show()
```

<figure><img src="../../../../../.gitbook/assets/image (84).png" alt=""><figcaption></figcaption></figure>

## Conclusiones

Como aparece en el histograma podemos identificar rápidamente que está sesgada hacia la derecha (o con la cola hacia la derecha). Esto indica que la mayor parte de la concentración de datos se encuentra al comienzo de la distribución.

En la caja Boxplot se ve como la mayoría de outliers por encima del límite superior.

###

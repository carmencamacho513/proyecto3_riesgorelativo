# Histograma-Boxplot mas90\_dias\_vencido Python

```python
mas90_dias_vencido = df['mas90_dias_vencido'].values

# Histograma
plt.figure(figsize=(10, 5))
plt.subplot(1, 2, 1) 
plt.hist(mas90_dias_vencido, bins=15, color='PaleVioletRed', alpha=0.7)
plt.title('Histograma de mas90_dias_vencido')
plt.xlabel('mas90_dias_vencido')
plt.ylabel('Frecuencia')

# Boxplot
plt.subplot(1, 2, 2) 
plt.boxplot(mas90_dias_vencido, vert=False, widths=0.7, patch_artist=True, boxprops=dict(facecolor='Pink'))
plt.title('Boxplot de mas90_dias_vencido')
plt.xlabel('mas90_dias_vencido')

# Gráficos
plt.tight_layout()
plt.show()
```

<figure><img src="../../../../../.gitbook/assets/image (86).png" alt=""><figcaption></figcaption></figure>

## Conclusiones

Como aparece en el histograma podemos identificar rápidamente que está sesgada hacia la derecha (o con la cola hacia la derecha). Esto indica que la mayor parte de la concentración de datos se encuentra al comienzo de la distribución.

En la caja Boxplot se ve como la mayoría de outliers porencima del límite superior.

###

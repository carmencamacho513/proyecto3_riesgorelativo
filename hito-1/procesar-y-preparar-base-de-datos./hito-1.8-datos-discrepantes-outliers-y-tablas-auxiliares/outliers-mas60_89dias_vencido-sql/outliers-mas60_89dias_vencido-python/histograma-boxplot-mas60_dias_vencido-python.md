# Histograma-Boxplot mas60\_dias\_vencido Python

```python
mas60_89dias_vencido = df['mas60_89dias_vencido'].values

# Histograma
plt.figure(figsize=(10, 5))
plt.subplot(1, 2, 1) 
plt.hist(mas60_89dias_vencido, bins=15, color='OrangeRed', alpha=0.7)
plt.title('Histograma de mas60_89dias_vencido')
plt.xlabel('mas60_89dias_vencido')
plt.ylabel('Frecuencia')

# Boxplot
plt.subplot(1, 2, 2) 
plt.boxplot(mas60_89dias_vencido, vert=False, widths=0.7, patch_artist=True, boxprops=dict(facecolor='DarkKhaki'))
plt.title('Boxplot de ratio_deuda')
plt.xlabel('ratio_deuda')

# Gráficos
plt.tight_layout()
plt.show()
```

<figure><img src="../../../../../.gitbook/assets/image (83).png" alt=""><figcaption></figcaption></figure>

## Conclusiones

Como aparece en el histograma podemos identificar rápidamente que está sesgada hacia la derecha (o con la cola hacia la derecha). Esto indica que la mayor parte de la concentración de datos se encuentra al comienzo de la distribución.

En la caja Boxplot se ve como la mayoría de outliers porencima del límite superior.

###

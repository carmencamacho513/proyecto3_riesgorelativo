# Histograma-Boxplot ultimo\_salario Python

```python
df = df.dropna(subset=['ultimo_salario'])
ultimo_salario = df['ultimo_salario'].values

# Histograma
plt.figure(figsize=(10, 5))
plt.subplot(1, 2, 1) 
plt.hist(ultimo_salario, bins=15, color='LightCoral', alpha=0.7)
plt.title('Histograma de Ultimo Salario')
plt.xlabel('Ultimo Salario')
plt.ylabel('Frecuencia')

# Boxplot
plt.subplot(1, 2, 2) 
plt.boxplot(ultimo_salario, vert=False, widths=0.7, patch_artist=True, boxprops=dict(facecolor='DeepSkyBlue'))
plt.title('Boxplot de Ultimo Salario')
plt.xlabel('Ultimo salario')

# Gráficos
plt.tight_layout()
plt.show()
```

<figure><img src="../../../../../.gitbook/assets/image (88).png" alt=""><figcaption></figcaption></figure>

## Conclusiones

Como aparece en el histograma podemos identificar rápidamente que está sesgada hacia la derecha (o con la cola hacia la derecha). Esto indica que la mayor parte de la concentración de sueldos se encuentra al comienzo de la distribución.

En la caja Boxplot se ve como la mayoría de outliers son sueldos altos por encima de 15.650 dolares .

###

# Histograma-Boxplot dependientes Python

```python
dependientes = df['dependientes'].values

# Histograma
plt.figure(figsize=(10, 5))
plt.subplot(1, 2, 1) 
plt.hist(dependientes, bins=15, color='Coral', alpha=0.7)
plt.title('Histograma de Dependientes')
plt.xlabel('Dependientes')
plt.ylabel('Frecuencia')

# Boxplot
plt.subplot(1, 2, 2) 
plt.boxplot(dependientes, vert=False, widths=0.7, patch_artist=True, boxprops=dict(facecolor='Orchid'))
plt.title('Boxplot de Dependientes')
plt.xlabel('Dependientes')

# Gráficos
plt.tight_layout()
plt.show()
```

<figure><img src="../../../../../.gitbook/assets/image (87).png" alt=""><figcaption></figcaption></figure>

## Conclusiones

Como aparece en el histograma podemos identificar rápidamente que está sesgada hacia la derecha (o con la cola hacia la derecha). Esto indica que la mayor parte de la concentración de dependientes se encuentra al comienzo de la distribución.

En la caja Boxplot se ve como la mayoría de outliers estan por encima del límite superior o dependientes mayores a 5 personas.

###

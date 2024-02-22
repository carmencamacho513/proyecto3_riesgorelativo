# Histograma-Boxplot otros\_prestamos Python

```sql
df = df.dropna(subset=['otros_prestamos'])
otros_prestamos = df['otros_prestamos'].values

# Histograma
plt.figure(figsize=(10, 5))
plt.subplot(1, 2, 1)
n, bins, patches = plt.hist(otros_prestamos, bins=15, color='MediumTurquoise', alpha=0.7, edgecolor='black')
plt.title('Histograma de otros_prestamos')
plt.xlabel('otros_prestamos')
plt.ylabel('Frecuencia')

# Mediana y Media
mediana = np.median(otros_prestamos)
media = np.mean(otros_prestamos)

# Añadir línea de mediana
plt.axvline(mediana, color='red', linestyle='dashed', linewidth=2, label=f'Mediana: {mediana:.2f}')

# Añadir línea de media
plt.axvline(media, color='green', linestyle='dashed', linewidth=2, label=f'Media: {media:.2f}')

plt.legend()

# Boxplot
plt.subplot(1, 2, 2)
plt.boxplot(otros_prestamos, vert=False, widths=0.7, patch_artist=True, boxprops=dict(facecolor='Peru'))
plt.title('Diagrama de caja de otros_prestamos')
plt.xlabel('otros_prestamos')

# Gráficos
plt.tight_layout()
plt.show()
```

<figure><img src="../../../../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

## Conclusiones

Como aparece en el histograma podemos identificar rápidamente que está sesgada hacia la derecha (o con la cola hacia la derecha). Esto indica que la mayor parte de la concentración de cantidad de otros creditos se encuentra al comienzo de la distribución.

En la caja Boxplot se ve como la mayoría de outliers estan por encima del límite superior o cantidad de otros creditos.

###

# Histograma-Boxplot real\_bienes Python

```sql
df = df.dropna(subset=['real_bienes'])
real_bienes = df['real_bienes'].values

# Histograma
plt.figure(figsize=(10, 5))
plt.subplot(1, 2, 1)
n, bins, patches = plt.hist(real_bienes, bins=15, color='OrangeRed', alpha=0.7, edgecolor='black')
plt.title('Histograma de real_bienes')
plt.xlabel('real_bienes')
plt.ylabel('Frecuencia')

# Mediana y Media
mediana = np.median(real_bienes)
media = np.mean(real_bienes)

# Añadir línea de mediana
plt.axvline(mediana, color='red', linestyle='dashed', linewidth=2, label=f'Mediana: {mediana:.2f}')

# Añadir línea de media
plt.axvline(media, color='green', linestyle='dashed', linewidth=2, label=f'Media: {media:.2f}')

plt.legend()

# Boxplot
plt.subplot(1, 2, 2)
plt.boxplot(real_bienes, vert=False, widths=0.7, patch_artist=True, boxprops=dict(facecolor='BlueViolet'))
plt.title('Diagrama de caja de real_bienes')
plt.xlabel('real_bienes')

# Gráficos
plt.tight_layout()
plt.show()
```

<figure><img src="../../../../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

## Conclusiones

Como aparece en el histograma podemos identificar rápidamente que está sesgada hacia la derecha (o con la cola hacia la derecha). Esto indica que la mayor parte de la concentración de cantidad de creditos se encuentra al comienzo de la distribución.

En la caja Boxplot se ve como la mayoría de outliers estan por encima del límite superior o cantidad de creditos.

###





##

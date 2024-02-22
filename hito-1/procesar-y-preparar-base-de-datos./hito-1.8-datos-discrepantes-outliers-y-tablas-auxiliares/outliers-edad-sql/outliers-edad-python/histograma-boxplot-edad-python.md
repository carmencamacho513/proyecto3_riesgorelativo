# Histograma-Boxplot edad Python

```python
edad = df['edad'].values

# Histograma
plt.figure(figsize=(10, 5))
plt.subplot(1, 2, 1) 
plt.hist(edad, bins=15, color='MediumVioletRed', alpha=0.7)
plt.title('Histograma de Edades')
plt.xlabel('Edad')
plt.ylabel('Frecuencia')

# Boxplot
plt.subplot(1, 2, 2) 
plt.boxplot(edad, vert=False, widths=0.7, patch_artist=True, boxprops=dict(facecolor='MediumSlateBlue'))
plt.title('Boxplot de Edades')
plt.xlabel('Edad')

# Gráficos
plt.tight_layout()
plt.show()
```

<figure><img src="../../../../../.gitbook/assets/image (89).png" alt=""><figcaption></figcaption></figure>

## Conclusiones

Como aparece en gráfica podemos identificar que es un histograma simétrico porque la mayoría de datos estan en el centro del gráfico.

En la caja Boxplot se ve como la mayoría de outliers son edades iguales o mayores a 97 años.

###

###

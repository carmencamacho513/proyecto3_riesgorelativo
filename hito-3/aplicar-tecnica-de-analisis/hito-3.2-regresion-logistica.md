# Hito 3.2 Regresión Logística

## Meta

Regresión logística.

## Objetivo

Calcular la propensión a ser un cliente con riesgo crediticio a partir de una regresión logística.

### OPRIME <mark style="color:red;">Google Colaboraty</mark> encuentras el Proceso.

{% embed url="https://colab.research.google.com/drive/12a4h89E1lInxIFgPQ7Gv9HZ5hHFQLvxj?usp=sharing" %}

#### Se importa dataframe de BigQuery donde se relizó las variables Dummies.

<figure><img src="../../.gitbook/assets/image (180).png" alt=""><figcaption></figcaption></figure>

### Regresión logística

#### Se realizó Regresión Logística donde la variable independiente es 'estado\_mora' y las dependientes son cada varible a estudio.

### Código de Regresión Logística



```python
X = df.drop('estado_mora', axis=1)  # Variables independientes
y = df['dummy_edad']  # Variable dependiente

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

scaler = StandardScaler()
X_train = scaler.fit_transform(X_train)
X_test = scaler.transform(X_test)

model = LogisticRegression()
model.fit(X_train, y_train)
```

```notebook-python
y_pred = model.predict(X_test)

print("Accuracy:", accuracy_score(y_test, y_pred))
print("Confusion Matrix:\n", confusion_matrix(y_test, y_pred))
print("Classification Report:\n", classification_report(y_test, y_pred))
```

<figure><img src="../../.gitbook/assets/image (181).png" alt=""><figcaption></figcaption></figure>

### Conclusiones

Este resultado pertenece a la evaluación de un modelo de clasificación de la variable 'edad';

1. **Accuracy (Precisión): 1.0**
   * La precisión es la proporción de predicciones correctas en relación con el total de predicciones.
   * Un valor de 1.0 (o 100%) significa que todas las predicciones del modelo fueron correctas.
2. **Confusion Matrix (Matriz de Confusión):**

* La matriz de confusión muestra la cantidad de predicciones correctas e incorrectas divididas en clases.
* En este caso, la clase 0 tiene 504 predicciones correctas y ninguna incorrecta. La clase 1 tiene 6696 predicciones correctas y ninguna incorrecta.

3. **Classification Report (Informe de Clasificación):**

* **Precision (Precisión):** La proporción de predicciones positivas correctas entre todas las predicciones positivas. Ambas clases tienen una precisión del 100%, lo que significa que todas las predicciones positivas son correctas.
* **Recall (Recuperación o Sensibilidad):** La proporción de instancias positivas correctamente identificadas en comparación con el total de instancias positivas. Al igual que la precisión, ambas clases tienen un recall del 100%.
* **F1-score:** Es una medida que combina precisión y recuperación en un solo número. Al ser 1.00 en ambas clases, indica un rendimiento perfecto.
* **Support (Soporte):** La cantidad de instancias de cada clase en los datos de prueba.

4. **Promedio Ponderado:**

* El informe muestra promedios ponderados para precision, recall y f1-score. Dado que todos los valores son 1.00 en ambas clases y hay un equilibrio en el soporte, los promedios ponderados también son 1.00.

#### En resumen, el modelo ha tenido un rendimiento perfecto en la clasificación de todas las varibles del estudio, con una precisión del 100% en ambas clases y ninguna predicción incorrecta.



### OPRIME <mark style="color:red;">En conceptos Obtenidos en el Proceso</mark> encuentras la definición de:

* Accuracy (Precisión)
* Confusion Matrix (Matriz de Confusión)
* Classification Report (Informe de Clasificación)
* Precision (Precisión)
* Recall (Recuperación o Sensibilidad)
* F1-score
* Support (Soporte)
* Promedio Ponderado



{% content-ref url="../../conceptos-obtenidos-en-el-proceso..md" %}
[conceptos-obtenidos-en-el-proceso..md](../../conceptos-obtenidos-en-el-proceso..md)
{% endcontent-ref %}


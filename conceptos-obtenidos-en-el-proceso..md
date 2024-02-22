# 📚 Conceptos Obtenidos en el Proceso.

* **El rango intercuartílico (IQR)** es una medida estadística que se utiliza para describir la dispersión o variabilidad en un conjunto de datos. Para calcular el IQR, primero necesitas ordenar tus datos de menor a mayor. Luego, divides tus datos en cuatro partes iguales, conocidas como cuartiles.

El IQR es la diferencia entre el tercer cuartil (Q3) y el primer cuartil (Q1). Matemáticamente, se expresa así:

$$IQR=Q3−Q1$$

Donde: $$Q1$$ es el valor que deja el 25% de los datos por debajo y el 75% por encima. $$Q3$$ es el valor que deja el 75% de los datos por debajo y el 25% por encima.

En resumen, el IQR te da una idea de la variabilidad en el 50% medio de tus datos, eliminando la influencia de los valores extremos. Es útil porque no se ve afectado por valores atípicos o extremos, proporcionando así una medida más robusta de la dispersión en comparación con el rango completo de los datos.

* **Histograma sesgado:** hacia la derecha es cuando la distribución de datos indica que los valores altos ocurren con baja frecuencia. Este modelo también se conoce comúnmente como el modelo de "cola derecha", ya que “se afina" a medida que nos movemos a lo largo del eje x, lo que indica que la frecuencia está disminuyendo.
* **Histograma simétrico** (o unimodal) centra los datos en la media (medida central) y tiene características a través de la distribución de la media y la desviación estándar. Una característica del histograma simétrico es contener la mayor cantidad de datos del centro del gráfico. En estadística, este modelo se llama normal y le permite analizar cuánto se desvían otros datos de este modelo.
*   **Un boxplot:** también conocido como diagrama de caja y bigotes, es una representación gráfica que muestra la distribución de un conjunto de datos. Este gráfico proporciona información sobre la mediana, los cuartiles y la presencia de posibles valores atípicos en los datos. El "caja" en el centro del gráfico representa el rango intercuartílico (IQR), que es la diferencia entre el primer cuartil (Q1) y el tercer cuartil (Q3). Los "bigotes" se extienden desde la caja hasta los valores extremos, pero generalmente no más allá de 1.5 veces el IQR.

    En resumen, un boxplot es una herramienta visual que ayuda a entender la dispersión y la distribución de un conjunto de datos, destacando aspectos clave como la mediana, los cuartiles y posibles valores atípicos.
* **El método Z-score:** también conocido como puntaje Z o estándar Z, es una medida estadística que cuantifica la posición de un punto de datos con respecto a la media de un conjunto de datos y expresa esa posición en términos de desviaciones estándar. Es una manera de normalizar los datos y compararlos en una escala común. El resultado Z indica cuántas desviaciones estándar un valor particular está por encima o por debajo de la media. Si el Z-score es positivo, significa que el valor está por encima de la media, y si es negativo, está por debajo de la media.
*   **Riesgo Relativo:**

    El riesgo relativo es una medida que se utiliza en estudios epidemiológicos para comparar la probabilidad de que un evento ocurra en dos grupos diferentes. Por lo general, se emplea en investigaciones sobre la relación entre un factor de riesgo (como fumar) y el desarrollo de una enfermedad. Se calcula dividiendo la tasa de incidencia del evento en el grupo expuesto al factor de riesgo entre la tasa de incidencia en el grupo no expuesto.

    La fórmula es la siguiente:  **Riesgo Relativo= Riesgo de incidencia en el grupo expuesto ​/  Riesgo de incidencia en el grupo no expuesto.**                                Un riesgo relativo igual a 1 indica que no hay diferencia en el riesgo entre ambos grupos. Un riesgo relativo mayor a 1 indica un mayor riesgo en el grupo expuesto, mientras que un riesgo relativo menor a 1 indica un menor riesgo en el grupo expuesto.
*   **Incidencia:**

    La incidencia se refiere a la frecuencia con la que ocurre un evento (como una enfermedad) en una población durante un período de tiempo específico. Se expresa como la tasa de incidencia, que es el número de nuevos casos de la enfermedad dividido por la población en riesgo durante ese período.

    La fórmula de la tasa de incidencia es: **Tasa de Incidencia=( Número de nuevos casos/Población de Riesgo) ​ ×1000**                                                             La incidencia proporciona una medida de la velocidad a la que ocurren los nuevos casos y es útil para evaluar la carga de enfermedad en una población.                                                                                                                       En resumen, el riesgo relativo compara las tasas de incidencia entre dos grupos, mientras que la incidencia en sí misma mide la frecuencia de un evento en una población. Ambos conceptos son fundamentales en la epidemiología para entender la relación entre factores de riesgo y enfermedades.
* **Univariado: Definición:** "Uni" significa uno, por lo que un análisis univariado se centra en una sola variable a la vez. **Enfoque:** Examina las características o propiedades de una única variable sin considerar ninguna relación con otras variables. **Ejemplo:** Si estudias la altura de un grupo de personas, un análisis univariado se centraría solo en la variable "altura" sin tener en cuenta ninguna otra característica.
* **Bivariado: Definición:** "Bi" significa dos, así que un análisis bivariado se enfoca en dos variables simultáneamente. **Enfoque:** Busca entender la relación o asociación entre dos variables, analizando cómo cambia una variable en función de la otra. **Ejemplo:** Si estudias la relación entre la cantidad de horas de estudio y las calificaciones obtenidas por los estudiantes, estás realizando un análisis bivariado.
* **Multivariado: Definición:** "Multi" significa muchos, por lo que un análisis multivariado implica el estudio simultáneo de tres o más variables. **Enfoque:** Examina las interacciones complejas entre múltiples variables, considerando cómo varias variables se relacionan entre sí de manera conjunta. **Ejemplo:** Si analizas la influencia de la cantidad de horas de estudio, el nivel de ansiedad y la calidad del sueño en el rendimiento académico, estás realizando un análisis multivariado.                                                                                                    **En resumen, univariado se enfoca en una variable, bivariado en dos variables para explorar su relación, y multivariado en tres o más variables para comprender las interacciones complejas entre ellas.**
*   **Variables Dummies: Definición:** Las variables dummy son creadas para representar información cualitativa, como categorías, grupos o características que no son numéricas. **Valores:** Estas variables toman solo dos valores posibles, generalmente 0 o 1. El valor 1 indica la presencia de la característica, mientras que el valor 0 indica su ausencia. **Ejemplo:** supongamos que estamos estudiando el impacto del tipo de combustible en el rendimiento de los automóviles. Podríamos crear una variable dummy llamada "Diesel" que tome el valor 1 si el automóvil funciona con diesel y 0 si no. De manera similar, podríamos tener otra variable dummy llamada "Gasolina" que tome el valor 1 si el automóvil funciona con gasolina y 0 si no. **Uso en Regresión:** En modelos de regresión, las variables dummy se utilizan para representar variables categóricas en términos numéricos, permitiendo que el modelo las incluya en sus cálculos. **Evitar Multicolinealidad:** Cuando se tienen varias categorías, es común usar una categoría como referencia y crear variables dummy para las demás categorías. Esto ayuda a evitar problemas de multicolinealidad en el modelo.

    **En resumen, las variables dummy son una manera de representar información cualitativa o categórica de manera numérica en análisis estadísticos, facilitando la inclusión de estas características en modelos matemáticos como los de regresión.**
* **Precisión (Accuracy):** La precisión se calcula como el número de predicciones correctas (verdaderos positivos más verdaderos negativos) dividido por el total de observaciones.
* **Matriz de confusión:** es una tabla que se utiliza en el campo de la clasificación para evaluar el rendimiento de un modelo predictivo. Se compone de cuatro celdas que representan la cantidad de observaciones clasificadas de acuerdo con su verdadero estado y su estado predicho por el modelo. Las cuatro celdas son:
* Verdaderos Positivos (VP): Observaciones que fueron clasificadas correctamente como positivas.
* Falsos Positivos (FP): Observaciones que fueron clasificadas incorrectamente como positivas.
* Verdaderos Negativos (VN): Observaciones que fueron clasificadas correctamente como negativas.
* Falsos Negativos (FN): Observaciones que fueron clasificadas incorrectamente como negativas.

**Permite visualizar cuántas predicciones fueron correctas o incorrectas en términos de positivos y negativos.**

* **Accuracy (Precisión): Significado:** Representa la proporción de predicciones correctas con respecto al total de predicciones del modelo. **Ejemplo:** Un valor de 1.0 significa que todas las predicciones del modelo fueron correctas, es decir, el 100% de precisión.
* **Confusion Matrix (Matriz de Confusión): Significado:** Una tabla que muestra la cantidad de predicciones correctas e incorrectas, divididas en clases. **Ejemplo:** En una matriz de confusión, se pueden ver cuántas predicciones fueron correctas para la clase 0 y la clase 1.
* **Classification Report (Informe de Clasificación): Significado:** Proporciona métricas detalladas de rendimiento del modelo, incluyendo precisión, recuperación (sensibilidad), F1-score y soporte. **Ejemplo:** Permite evaluar no solo la precisión general, sino también el rendimiento específico para cada clase.
* **Precision (Precisión): Significado:** Indica la proporción de predicciones positivas correctas entre todas las predicciones positivas. **Ejemplo:** Una precisión del 100% significa que todas las predicciones positivas del modelo son correctas.
* **Recall (Recuperación o Sensibilidad): Significado:** Muestra la proporción de instancias positivas correctamente identificadas en comparación con el total de instancias positivas. **Ejemplo:** Un recall del 100% indica que el modelo identifica todas las instancias positivas.
* **F1-score: Significado:** Es una métrica que combina precisión y recuperación en un solo número. Es útil cuando hay un desequilibrio en las clases. **Ejemplo:** Un F1-score de 1.0 indica un rendimiento perfecto, mientras que valores más bajos sugieren un equilibrio entre precisión y recuperación.
* **Support (Soporte): Significado:** La cantidad de instancias de cada clase en los datos de prueba. **Ejemplo:** Puede indicar si hay un desequilibrio en la distribución de las clases en el conjunto de datos.
* **Promedio Ponderado: Significado:** Se refiere al promedio ponderado de las métricas, donde se tiene en cuenta el soporte de cada clase. **Ejemplo:** Si hay más instancias de una clase, su rendimiento tendrá más peso en el promedio ponderado.

\


\

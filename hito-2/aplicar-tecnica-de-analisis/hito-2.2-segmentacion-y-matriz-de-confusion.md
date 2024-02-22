# Hito 2.2 Segmentación y Matriz de Confusión

## Meta

Segmentación

## Objetivo

Calcular el score de riesgo por cada cliente y utilizar este score para clasificarlos entre buen y mal pagador.



```sql
WITH dummys AS (
  SELECT
    user_id,
    estado_mora,
    IF(cuartil_edad IN (1, 2, 3), 1, 0) AS dummy_edad,  
    IF(cuartil_dependientes IN (1, 2, 3), 1, 0) AS dummy_dependientes,
    IF(cuartil_credito IN (1, 2, 3), 1, 0) AS dummy_credito,
    IF(cuartil_mas90 IN (1, 2, 3), 1, 0) AS dummy_mas90,
    IF(cuartil_ratio IN (1, 2, 3), 1, 0) AS dummy_ratio,
    IF(cuartil_salario IN (1, 2, 3), 1, 0) AS dummy_salario
  FROM
    `riesgo-relativo-proyecto-3.super_cajaTwo.cuartil_dummys`
),
score AS (
  SELECT
    user_id,
    estado_mora,
    dummy_edad + dummy_dependientes + dummy_credito + dummy_mas90 + dummy_ratio + dummy_salario AS score
  FROM
    dummys
)
SELECT
  dummys.*,
  score.score,
  CASE
    WHEN dummys.estado_mora = 1 AND score.score > 3 THEN 1  
    WHEN dummys.estado_mora = 0 AND score.score <= 3 THEN 1  
    ELSE 0  
  END AS correct_prediction
FROM
  dummys
JOIN
  score
ON
  dummys.user_id = score.user_id;
```

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

### Matriz de Confusión

```sql
SELECT
  COUNTIF(estado_mora = 1 AND correct_prediction
 = 1) AS verdaderos_positivos,
  COUNTIF(estado_mora = 0 AND correct_prediction
 = 1) AS falsos_positivos,
  COUNTIF(estado_mora = 1 AND correct_prediction
 = 0) AS falsos_negativos,
  COUNTIF(estado_mora = 0 AND correct_prediction
 = 0) AS verdaderos_negativos
FROM
  `riesgo-relativo-proyecto-3.super_cajaTwo.total_score`
```

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

### Precisión de Modelo

```sql
WITH dummys AS (
  SELECT
    user_id,
    estado_mora,
    IF(cuartil_edad IN (1, 2, 3), 1, 0) AS dummy_edad,  
    IF(cuartil_dependientes IN (1, 2, 3), 1, 0) AS dummy_dependientes,
    IF(cuartil_credito IN (1, 2, 3), 1, 0) AS dummy_credito,
    IF(cuartil_mas90 IN (1, 2, 3), 1, 0) AS dummy_mas90,
    IF(cuartil_ratio IN (1, 2, 3), 1, 0) AS dummy_ratio,
    IF(cuartil_salario IN (1, 2, 3), 1, 0) AS dummy_salario
  FROM
    `riesgo-relativo-proyecto-3.super_cajaTwo.cuartil_dummys`
),
score AS (
  SELECT
    user_id,
    estado_mora,
    dummy_edad + dummy_dependientes + dummy_credito + dummy_mas90 + dummy_ratio + dummy_salario AS score
  FROM
    dummys
),
predictions AS (
  SELECT
    dummys.*,
    score.score,
    CASE
      WHEN dummys.estado_mora = 1 AND score.score > 3 THEN 1  
      WHEN dummys.estado_mora = 0 AND score.score <= 3 THEN 1  
      ELSE 0  
    END AS correct_prediction
  FROM
    dummys
  JOIN
    score
  ON
    dummys.user_id = score.user_id
)
SELECT
  COUNTIF(correct_prediction = 1) / COUNT(*) AS precision
FROM
  predictions;
```

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

### Conclusiones

Se realizó el calculo del score de riesgo por cada cliente y se utilizó score para clasificarlos entre buen y mal pagador.

**Precisión de Modelo:** Se utilizó Precisión (Accuracy)**:** dio como resultado 0.0911 significa que el modelo clasificó correctamente aproximadamente el 9.11% de las observaciones del conjunto de datos.

#### **Matriz de Confusión**

1. **Verdaderos Positivos (True Positives - TP):** 525
   * Representa la cantidad de casos en los que el modelo y la realidad coinciden al predecir que el "estado de mora" es 1 y el "correct\_prediction" es 1. En otras palabras, el modelo acertó al identificar correctamente un caso positivo.
2. **Falsos Positivos (False Positives - FP):** 2755
   * Indica la cantidad de casos en los que el modelo predijo incorrectamente que el "estado de mora" es 1 (positivo), pero el "correct\_prediction" es 0 (negativo). Es un error en el que el modelo indicó una mora cuando en realidad no la hay.
3. **Falsos Negativos (False Negatives - FN):** 158
   * Muestra la cantidad de casos en los que el modelo predijo incorrectamente que el "estado de mora" es 0 (negativo), pero el "correct\_prediction" es 1 (positivo). Es un error en el que el modelo no identificó correctamente los casos positivos reales.
4. **Verdaderos Negativos (True Negatives - TN):** 32562
   * Representa la cantidad de casos en los que el modelo y la realidad coinciden al predecir que el "estado de mora" es 0 y el "correct\_prediction" es 0. El modelo acertó al identificar correctamente un caso negativo.



### OPRIME <mark style="color:red;">En conceptos Obtenidos en el Proceso</mark> encuentras la definición de **Precisión (Accuracy) y Matriz de Confusión**: 

{% content-ref url="../../conceptos-obtenidos-en-el-proceso..md" %}
[conceptos-obtenidos-en-el-proceso..md](../../conceptos-obtenidos-en-el-proceso..md)
{% endcontent-ref %}

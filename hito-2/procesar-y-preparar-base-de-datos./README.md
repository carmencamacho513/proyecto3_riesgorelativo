# 💪 Procesar y Preparar Base de Datos.

Google Colab.

```googlesql
WITH dummys AS (
  SELECT
    user_id,
    estado_mora,
    IF(edad = 3, 1, 0) AS dummy_edad,  
    IF(dependientes > 2, 1, 0) AS dummy_dependientes,
    IF(limite_credito_personal = 3, 1, 0) AS dummy_credito,
    IF(mas90_dias_vencido = 3, 1, 0) AS dummy_mas90,
    IF(ratio_deuda = 3, 1, 0) AS dummy_ratio,
    IF(ultimo_salario = 3, 1, 0) AS dummy_salario
  FROM
    `riesgo-relativo-proyecto-3.super_cajaTwo.super_cajaGeneral`
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
  IF(score.score >= 5, 1, 0) AS total_score
FROM
  dummys
JOIN
  score
ON
  dummys.user_id = score.user_id;
```

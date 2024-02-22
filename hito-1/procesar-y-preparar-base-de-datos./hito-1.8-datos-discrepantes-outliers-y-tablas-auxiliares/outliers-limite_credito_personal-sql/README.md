# Outliers limite\_credito\_personal SQL

```sql
WITH
  Quartiles AS (
    SELECT
      APPROX_QUANTILES(limite_credito_personal, 4)[SAFE_OFFSET(1)] AS q1,
      APPROX_QUANTILES(limite_credito_personal, 4)[SAFE_OFFSET(3)] AS q3
    FROM
      `riesgo-relativo-proyecto-3.super_cajaTwo.super_cajaGeneral`
  )

SELECT
  t.*, 
  q.q3 - q.q1 AS iqr,
  q.q1 - 1.5 * (q.q3 - q.q1) AS limite_inferior,
  q.q3 + 1.5 * (q.q3 - q.q1) AS limite_superior,
  CASE
    WHEN t.limite_credito_personal < q.q1 - 1.5 * (q.q3 - q.q1) OR t.limite_credito_personal > q.q3 + 1.5 * (q.q3 - q.q1) THEN 'Si es Outlier'
    ELSE 'No es Outlier'
  END AS outlier_limite_credito_personal
FROM
  `riesgo-relativo-proyecto-3.super_cajaTwo.super_cajaGeneral` AS t
CROSS JOIN
  Quartiles q;
```

<figure><img src="../../../../.gitbook/assets/image (62).png" alt=""><figcaption></figcaption></figure>

## Conclusiones

Se realiza una tabla temporal con **With** y una "gráfico de caja y bigotes" utiliza los cuartiles, se calcula el límite inferior (- 1.5) y el limite superior (+ 1.5) para identificar Outliers utilizando el rango intercuartílico. &#x20;

Como resultado nos retorna que los límites y el IQR estan en 0. La función `APPROX_QUANTILES` no está calculando los cuartiles correctamente debido a la distribución de los datos y utiliza aproximaciones para calcular los cuartiles y puede no ser precisa en ciertos casos.

Por esto realizamos los calculos en Python.



###

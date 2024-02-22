# Outliers Ratio Deuda SQL

```sql
WITH
  Quartiles AS (
  SELECT
    APPROX_QUANTILES(ratio_deuda, 4)[SAFE_OFFSET(1)] AS q1,
    APPROX_QUANTILES(ratio_deuda, 4)[SAFE_OFFSET(3)] AS q3
  FROM
    `riesgo-relativo-proyecto-3.super_cajaTwo.super_cajaGeneral` )
SELECT
  t.*,
  q.q3 - q.q1 AS iqr,
  q.q1 - 1.5 * (q.q3 - q.q1) AS limite_inferior,
  q.q3 + 1.5 * (q.q3 - q.q1) AS limite_superior,
  CASE
    WHEN t.ratio_deuda < q.q1 - 1.5 * (q.q3 - q.q1) OR t.ratio_deuda > q.q3 + 1.5 * (q.q3 - q.q1) THEN 'Si es Outlier'
  ELSE
  'No es Outlier'
END
  AS outlier_ratio
FROM
  `riesgo-relativo-proyecto-3.super_cajaTwo.super_cajaGeneral` AS t
CROSS JOIN
  Quartiles q;
```

```sql
SELECT
  outlier_ratio,
  COUNT(*) AS cantidad
FROM
  `riesgo-relativo-proyecto-3.super_cajaTwo.outliers_ratio`
WHERE
  outlier_ratio IN ('Si es Outlier', 'No es Outlier')
GROUP BY
  outlier_ratio;
```

<figure><img src="../../../../.gitbook/assets/image (112).png" alt=""><figcaption></figcaption></figure>

```sql
SELECT
  outlier_ratio,
  COUNT(*) AS cantidad,
  COUNT(CASE WHEN ultimo_salario IS NULL THEN 1 END) AS cantidadNulos_salario,
  COUNT(CASE WHEN estado_mora = 1 THEN 1 END) AS cantidad_malaPaga,
  COUNT(CASE WHEN estado_mora = 0 THEN 1 END) AS cantidad_buenaPaga,
FROM
  `riesgo-relativo-proyecto-3.super_cajaTwo.outliers_ratio`
WHERE
  outlier_ratio IN ('Si es Outlier', 'No es Outlier')
GROUP BY
 outlier_ratio;
```

<figure><img src="../../../../.gitbook/assets/image (113).png" alt=""><figcaption></figcaption></figure>

## Conclusiones

Se realiza una sentencia con cuartiles y se calcula el límite inferior (- 1.5) y el limite superior (+ 1.5) para identificar Outliers utilizando el rango intercuartílico. Cualquier valor que esté por debajo del límite inferior o por encima del límite superior se considera un Outlier. Se renombra una columna la cual identifica 'Si es Outlier' o 'No es Outlier'. Luego se cuenta cuantos si son Outliers, cuantos de esos en la variable estado\_mora 1 son malos pagadores 0 si son buenos pagadores y de la variable ultimo\_salario son nulos.

Se encuentra que hay 7570 que si son Outliers y de esos 129 son malos pagadores, 7441 son buenos pagadores y hay 6774 nulo de la variable de ultimo\_salario.



###

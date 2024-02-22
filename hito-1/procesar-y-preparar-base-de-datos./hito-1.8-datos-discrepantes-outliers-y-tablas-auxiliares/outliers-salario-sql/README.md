# Outliers Salario SQL

```sql
WITH
  Quartiles AS (
    SELECT
      APPROX_QUANTILES(ultimo_salario, 4)[SAFE_OFFSET(1)] AS q1,
      APPROX_QUANTILES(ultimo_salario, 4)[SAFE_OFFSET(3)] AS q3
    FROM
      `riesgo-relativo-proyecto-3.super_cajaTwo.super_cajaGeneral`
  )

SELECT
  t.*, 
  q.q3 - q.q1 AS iqr,
  q.q1 - 1.5 * (q.q3 - q.q1) AS limite_inferior,
  q.q3 + 1.5 * (q.q3 - q.q1) AS limite_superior,
  CASE
    WHEN t.ultimo_salario < q.q1 - 1.5 * (q.q3 - q.q1) OR t.ultimo_salario > q.q3 + 1.5 * (q.q3 - q.q1) THEN 'Si es Outlier'
    ELSE 'No es Outlier'
  END AS outlier_salario
FROM
  `riesgo-relativo-proyecto-3.super_cajaTwo.super_cajaGeneral` AS t
CROSS JOIN
  Quartiles q;
```

<figure><img src="../../../../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

```sql
SELECT
  outlier_salario,
  COUNT(*) AS cantidad
FROM
  `riesgo-relativo-proyecto-3.super_cajaTwo.outliers_salario`
WHERE
  outlier_salario IN ('Si es Outlier', 'No es Outlier')
GROUP BY
  outlier_salario;
```

<figure><img src="../../../../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

```sql
SELECT
  outlier_salario,
  COUNT(*) AS cantidad,
  COUNT(CASE WHEN ultimo_salario IS NULL THEN 1 END) AS cantidad_salario,
  COUNT(CASE WHEN estado_mora = 1 THEN 1 END) AS cantidad_malaPaga,
  COUNT(CASE WHEN estado_mora = 0 THEN 1 END) AS cantidad_buenaPaga,
FROM
  `riesgo-relativo-proyecto-3.super_cajaTwo.outliers_salario`
WHERE
  outlier_salario IN ('Si es Outlier', 'No es Outlier')
GROUP BY
  outlier_salario;
```

<figure><img src="../../../../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>

## Conclusiones

Se realiza una tabla temporal con **With** y una "gráfico de caja y bigotes"utiliza los cuartiles, se calcula el límite inferior (- 1.5) y el limite superior (+ 1.5) para identificar Outliers utilizando el rango intercuartílico.  Cualquier valor que esté por debajo del límite inferior o por encima del límite superior se considera un Outlier o posibles valores atípicos. Se renombra una columna la cual identifica 'Si es Outlier' o 'No es Outlier'. Luego se cuenta cuantos si son Outliers, cuantos de esos en la variable estado\_mora 1 son malos pagadores 0 si son buenos pagadores y de la variable ultimo\_salario son nulos.

Se encuentra que hay 1174 que si son Outliers y de esos 7 son malos pagadores, 1167 son buenos pagadores y no hay ningunos nulo de la variable de ultimo\_salario.



###

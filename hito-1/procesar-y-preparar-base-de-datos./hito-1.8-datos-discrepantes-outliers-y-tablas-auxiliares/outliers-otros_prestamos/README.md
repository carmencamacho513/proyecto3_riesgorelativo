# Outliers otros\_prestamos

```sql
WITH
  Quartiles AS (
  SELECT
    APPROX_QUANTILES(otros_prestamos, 4)[SAFE_OFFSET(1)] AS q1,
    APPROX_QUANTILES(otros_prestamos, 4)[SAFE_OFFSET(3)] AS q3
  FROM
    `riesgo-relativo-proyecto-3.super_cajaTwo.super_cajaGeneral` )
SELECT
  t.*,
  q.q3 - q.q1 AS iqr,
  q.q1 - 1.5 * (q.q3 - q.q1) AS limite_inferior,
  q.q3 + 1.5 * (q.q3 - q.q1) AS limite_superior,
  CASE
    WHEN t.otros_prestamos < q.q1 - 1.5 * (q.q3 - q.q1) OR t.otros_prestamos > q.q3 + 1.5 * (q.q3 - q.q1) THEN 'Si es Outlier'
  ELSE
  'No es Outlier'
END
  AS outlier_otros_prestamos
FROM
  `riesgo-relativo-proyecto-3.super_cajaTwo.super_cajaGeneral` AS t
CROSS JOIN
  Quartiles q;
```

<figure><img src="../../../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

## Conclusiones

Se realiza una tabla temporal con **With** y una "gráfico de caja y bigotes" utiliza los cuartiles, se calcula el límite inferior (- 1.5) y el limite superior (+ 1.5) para identificar Outliers utilizando el rango intercuartílico. &#x20;

Como resultado nos retorna que los outliers estan por debajo del límite inferior -5 y por encima del límite superior 19.



###

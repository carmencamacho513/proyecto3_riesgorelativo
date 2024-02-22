# Riesgo Relativo Ratio de Deuda

```sql
WITH DatosConCuartiles AS (
  SELECT
    ratio_deuda,
    estado_mora,
    CASE
      WHEN ratio_deuda BETWEEN 0 AND 0.195110482 THEN 1
      WHEN ratio_deuda BETWEEN 0.195140307
    AND 0.382692908 THEN 2
      WHEN ratio_deuda BETWEEN 0.382700903 AND 0.968784838 THEN 3
      WHEN ratio_deuda BETWEEN 0.97009911
    AND 307001 THEN 4
    ELSE
    NULL
    END AS cuartil
  FROM
    `riesgo-relativo-proyecto-3.super_cajaTwo.super_cajaGeneral`
)
, DatosConLimitesRatio AS (
  SELECT
    dc.ratio_deuda,
    dc.estado_mora,
    dc.cuartil,
    CASE
      WHEN cuartil = 1 THEN 'Cuartil 1 (0 a 0.195110482 Ratio Deuda)'
      WHEN cuartil = 2 THEN 'Cuartil 2 (0.195140307 a 0.382692908 Ratio Deuda)'
      WHEN cuartil = 3 THEN 'Cuartil 3 (0.382700903 a 0.968784838 Ratio Deuda)'
      WHEN cuartil = 4 THEN 'Cuartil 4 (0.97009911 a 307001 Ratio Deuda)'
    ELSE
    'Fuera de Rango'
    END AS ratio_cuartil
  FROM
    DatosConCuartiles dc
)
, IncidenciaExpuesto AS (
  SELECT
    cuartil,
    COUNT(*) AS casos_expuesto,
    COUNT(DISTINCT ratio_deuda) AS poblacion_expuesto
  FROM
    DatosConLimitesRatio
  WHERE
    estado_mora = 1 
  GROUP BY
    cuartil
)
, IncidenciaNoExpuesto AS (
  SELECT
    cuartil,
    COUNT(*) AS casos_no_expuesto,
    COUNT(DISTINCT ratio_deuda) AS poblacion_no_expuesto
  FROM
    DatosConLimitesRatio
  WHERE
    estado_mora = 0 
  GROUP BY
    cuartil
)
SELECT
  dcl.cuartil,
  dcl.ratio_cuartil,
  COUNTIF(dcl.estado_mora = 0) AS ratio_buenos_pagadores,
  COUNTIF(dcl.estado_mora = 1) AS ratio_malos_pagadores,
  SUM(ie.casos_expuesto) AS ratio_casos_expuesto, 
  SUM(ine.casos_no_expuesto) AS ratio_casos_no_expuesto, 
  (SUM(ie.casos_expuesto) * 1.0 / SUM(ie.poblacion_expuesto)) / (SUM(ine.casos_no_expuesto) * 1.0 / SUM(ine.poblacion_no_expuesto)) AS ratio_riesgo_relativo
FROM
  DatosConLimitesRatio dcl
LEFT JOIN
  IncidenciaExpuesto ie ON dcl.cuartil = ie.cuartil
LEFT JOIN
  IncidenciaNoExpuesto ine ON dcl.cuartil = ine.cuartil
WHERE
  dcl.cuartil IS NOT NULL
GROUP BY
  dcl.cuartil, dcl.ratio_cuartil
ORDER BY
  dcl.cuartil;
```

<figure><img src="../../../.gitbook/assets/image (175).png" alt=""><figcaption></figcaption></figure>

### Resultado de Estudio

**Cuartil 1 (0 a 0.195110482 Ratio Deuda):**

* **Buenos Pagadores:** 9,725
* **Malos Pagadores:** 180
* **Total de Casos Expuestos:** 1,782,900
* **Total de Casos No Expuestos:** 96,326,125
* **Riesgo Relativo:** 1.0621

### Observación

En este grupo con un rango bajo de Ratio Deuda (Cuartil 1), el 1.0621 indica que hay aproximadamente 1.06 veces más riesgo relativo de ser un mal pagador en comparación con los no expuestos.

**Cuartil 2 (0.195140307 a 0.382692908 Ratio Deuda):**

* **Buenos Pagadores:** 8,638
* **Malos Pagadores:** 133
* **Total de Casos Expuestos:** 1,166,543
* **Total de Casos No Expuestos:** 75,763,898
* **Riesgo Relativo:** 0.9843

### Observación

En este grupo con un rango medio de Ratio Deuda (Cuartil 2), el 0.9843 indica que no hay un riesgo significativo adicional de ser un mal pagador en comparación con los no expuestos.

**Cuartil 3 (0.382700903 a 0.968784838 Ratio Deuda):**

* **Buenos Pagadores:** 8,504
* **Malos Pagadores:** 210
* **Total de Casos Expuestos:** 1,829,940
* **Total de Casos No Expuestos:** 74,103,856
* **Riesgo Relativo:** 0.9909

### Observación

En este grupo con un rango medio-alto de Ratio Deuda (Cuartil 3), el 0.9909 indica que no hay un riesgo significativo adicional de ser un mal pagador en comparación con los no expuestos.

**Cuartil 4 (0.97009911 a 307001 Ratio Deuda):**

* **Buenos Pagadores:** 8,449
* **Malos Pagadores:** 160
* **Total de Casos Expuestos:** 1,377,440
* **Total de Casos No Expuestos:** 72,737,441
* **Riesgo Relativo:** 0.5681

### Observación

En este grupo con un rango alto de Ratio Deuda (Cuartil 4), el 0.5681 indica que hay aproximadamente 0.57 veces menos riesgo relativo de ser un mal pagador en comparación con los no expuestos.

### Conclusiones

Se realizó una comparación del riesgo relativo de ser un mal pagador en diferentes grupos según el ratio de deuda. El riesgo relativo varía en cada cuartil, indicando cómo el rango de ratio de deuda afecta la probabilidad de ser un mal pagador en comparación con los no expuestos.

\

















# Riesgo Relativo otros\_prestamos

```sql
WITH DatosConCuartiles AS (
  SELECT
    otros_prestamos,
    estado_mora,
    CASE
      WHEN otros_prestamos BETWEEN 0 AND 12 THEN 1
      WHEN otros_prestamos BETWEEN 13 AND 25 THEN 2
      WHEN otros_prestamos BETWEEN 26 AND 38 THEN 3
      WHEN otros_prestamos BETWEEN 39 AND 56 THEN 4
      ELSE NULL
    END AS cuartil
  FROM
    `riesgo-relativo-proyecto-3.super_cajaTwo.super_cajaGeneral`
)
, DatosConLimitesOtros AS (
  SELECT
    dc.otros_prestamos,
    dc.estado_mora,
    dc.cuartil,
    CASE
      WHEN cuartil = 1 THEN 'Cuartil 1 (0 a 12 Total Otros Credito)'
      WHEN cuartil = 2 THEN 'Cuartil 2 (13 a 25 Total Otros Credito)'
      WHEN cuartil = 3 THEN 'Cuartil 3 (26 a 38 Total Otros Credito)'
      WHEN cuartil = 4 THEN 'Cuartil 4 (39 a 56 Total Otros Credito)'
      ELSE 'Fuera de Rango'
    END AS nombre_cuartil
  FROM
    DatosConCuartiles dc
)
, IncidenciaExpuesto AS (
  SELECT
    cuartil,
    COUNT(*) AS casos_expuesto,
    COUNT(DISTINCT otros_prestamos) AS poblacion_expuesto
  FROM
    DatosConLimitesOtros
  WHERE
    estado_mora = 1 
  GROUP BY
    cuartil
)
, IncidenciaNoExpuesto AS (
  SELECT
    cuartil,
    COUNT(*) AS casos_no_expuesto,
    COUNT(DISTINCT otros_prestamos) AS poblacion_no_expuesto
  FROM
    DatosConLimitesOtros
  WHERE
    estado_mora = 0 
  GROUP BY
    cuartil
)
SELECT
  dcl.cuartil,
  dcl.nombre_cuartil,
  COUNTIF(dcl.estado_mora = 0) AS buenos_pagadores,
  COUNTIF(dcl.estado_mora = 1) AS malos_pagadores,
  SUM(ie.casos_expuesto) AS total_casos_expuesto, 
  SUM(ine.casos_no_expuesto) AS total_casos_no_expuesto, 
  (SUM(ie.casos_expuesto) * 1.0 / SUM(ie.poblacion_expuesto)) / (SUM(ine.casos_no_expuesto) * 1.0 / SUM(ine.poblacion_no_expuesto)) AS riesgo_relativo
FROM
  DatosConLimitesOtros dcl
LEFT JOIN
  IncidenciaExpuesto ie ON dcl.cuartil = ie.cuartil
LEFT JOIN
  IncidenciaNoExpuesto ine ON dcl.cuartil = ine.cuartil
WHERE
  dcl.cuartil IS NOT NULL
GROUP BY
  dcl.cuartil, dcl.nombre_cuartil
ORDER BY
  dcl.cuartil;
```

<figure><img src="../../../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

**Resultado de Estudio**

**Cuartil 1 (0 a 12 Total Otros Créditos):**

* **Buenos Pagadores:** 30,211
* **Malos Pagadores:** 569
* **Total de Casos Expuestos:** 17,513,820
* **Total de Casos No Expuestos:** 929,894,580
* **Riesgo Relativo:** 0.0188

### Observación

En este grupo con 0 a 12 créditos adicionales (Cuartil 1), el riesgo relativo es bajo (0.0188), indicando que hay una probabilidad baja de ser un mal pagador en comparación con los no expuestos.

**Cuartil 2 (13 a 25 Total Otros Créditos):**

* **Buenos Pagadores:** 4,556
* **Malos Pagadores:** 51
* **Total de Casos Expuestos:** 234,957
* **Total de Casos No Expuestos:** 20,989,492
* **Riesgo Relativo:** 0.0146

### Observación

En este grupo con 13 a 25 créditos adicionales (Cuartil 2), el riesgo relativo es bajo (0.0146), indicando que hay una probabilidad baja de ser un mal pagador en comparación con los no expuestos.

**Cuartil 3 (26 a 38 Total Otros Créditos):**

* **Buenos Pagadores:** 164
* **Malos Pagadores:** 2
* **Total de Casos Expuestos:** 332
* **Total de Casos No Expuestos:** 27,224
* **Riesgo Relativo:** 0.0793

### Observación

En este grupo con 26 a 38 créditos adicionales (Cuartil 3), el riesgo relativo es moderadamente alto (0.0793), indicando que hay una probabilidad moderada alta de ser un mal pagador en comparación con los no expuestos.

**Cuartil 4 (39 a 56 Total Otros Créditos):**

* **Buenos Pagadores:** 22
* **Malos Pagadores:** 0
* **Total de Casos Expuestos:** No proporcionado (null)
* **Total de Casos No Expuestos:** 484
* **Riesgo Relativo:** No calculado (null)

### Observación

En este grupo con 39 a 56 créditos adicionales (Cuartil 4), no se proporciona información sobre el riesgo relativo debido a la falta de casos malos pagadores en este grupo.

### Conclusiones

Se realizó una comparación del riesgo relativo de ser un mal pagador en diferentes grupos según la cantidad de créditos adicionales. El riesgo relativo varía en cada cuartil, indicando cómo el rango de créditos adicionales afecta la probabilidad de ser un mal pagador en comparación con los no expuestos.

\

# Riesgo Relativo real\_bienes

```sql
WITH DatosConCuartiles AS (
  SELECT
    real_bienes,
    estado_mora,
    CASE
      WHEN real_bienes BETWEEN 0 AND 0 THEN 1
      WHEN real_bienes BETWEEN 1 AND 1 THEN 2
      WHEN real_bienes BETWEEN 2 AND 2 THEN 3
      WHEN real_bienes BETWEEN 3 AND 25 THEN 4
      ELSE NULL
    END AS cuartil
  FROM
    `riesgo-relativo-proyecto-3.super_cajaTwo.super_cajaGeneral`
)
, DatosConLimitesReal AS (
  SELECT
    dc.real_bienes,
    dc.estado_mora,
    dc.cuartil,
   CASE
      WHEN cuartil = 1 THEN 'Cuartil 1 (0 Creditos Inmobiliarios)'
      WHEN cuartil = 2 THEN 'Cuartil 2 (1 Creditos Inmobiliarios)'
      WHEN cuartil = 3 THEN 'Cuartil 3 (2 Creditos Inmobiliarios)'
      WHEN cuartil = 4 THEN 'Cuartil 4 (3 a 25 Creditos Inmobiliarios)'
      ELSE 'Fuera de Rango'
    END AS nombre_cuartil
  FROM
    DatosConCuartiles dc
)
, IncidenciaExpuesto AS (
  SELECT
    cuartil,
    COUNT(*) AS casos_expuesto,
    COUNT(DISTINCT real_bienes) AS poblacion_expuesto
  FROM
    DatosConLimitesReal
  WHERE
    estado_mora = 1 
  GROUP BY
    cuartil
)
, IncidenciaNoExpuesto AS (
  SELECT
    cuartil,
    COUNT(*) AS casos_no_expuesto,
    COUNT(DISTINCT real_bienes) AS poblacion_no_expuesto
  FROM
    DatosConLimitesReal
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
  DatosConLimitesReal dcl
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

<figure><img src="../../../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

### Resultado de Estudio

**Cuartil 1 (0 Créditos Inmobiliarios):**

* **Buenos Pagadores:** 12,791
* **Malos Pagadores:** 328
* **Total de Casos Expuestos:** 4,303,032
* **Total de Casos No Expuestos:** 167,805,129
* **Riesgo Relativo:** 0.0256

### Observación

En este grupo sin créditos inmobiliarios (Cuartil 1), el riesgo relativo es bajo (0.0256), indicando que hay una probabilidad muy baja de ser un mal pagador en comparación con los no expuestos.

**Cuartil 2 (1 Crédito Inmobiliario):**

* **Buenos Pagadores:** 12,373
* **Malos Pagadores:** 173
* **Total de Casos Expuestos:** 2,170,458
* **Total de Casos No Expuestos:** 155,231,658
* **Riesgo Relativo:** 0.0140

### Observación

En este grupo con 1 crédito inmobiliario (Cuartil 2), el riesgo relativo es bajo (0.0140), indicando que hay una probabilidad baja de ser un mal pagador en comparación con los no expuestos.

**Cuartil 3 (2 Créditos Inmobiliarios):**

* **Buenos Pagadores:** 7,426
* **Malos Pagadores:** 87
* **Total de Casos Expuestos:** 653,631
* **Total de Casos No Expuestos:** 55,791,538
* **Riesgo Relativo:** 0.0117

### Observación

En este grupo con 2 créditos inmobiliarios (Cuartil 3), el riesgo relativo es bajo (0.0117), indicando que hay una probabilidad baja de ser un mal pagador en comparación con los no expuestos.

**Cuartil 4 (3 a 25 Créditos Inmobiliarios):**

* **Buenos Pagadores:** 2,363
* **Malos Pagadores:** 34
* **Total de Casos Expuestos:** 81,498
* **Total de Casos No Expuestos:** 5,664,111
* **Riesgo Relativo:** 0.0324

### Observación

En este grupo con 3 a 25 créditos inmobiliarios (Cuartil 4), el riesgo relativo es moderadamente bajo (0.0324), indicando que hay una probabilidad moderada baja de ser un mal pagador en comparación con los no expuestos.

### Conclusiones

Se realizó una comparación del riesgo relativo de ser un mal pagador en diferentes grupos según la cantidad de créditos inmobiliarios. El riesgo relativo varía en cada cuartil, indicando cómo el rango de créditos inmobiliarios afecta la probabilidad de ser un mal pagador en comparación con los no expuestos.

\

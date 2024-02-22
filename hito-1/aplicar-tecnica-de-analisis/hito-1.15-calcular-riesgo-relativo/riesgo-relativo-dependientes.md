# Riesgo Relativo Dependientes

```sql
WITH DatosConCuartiles AS (
  SELECT
    dependientes,
    estado_mora,
    CASE
      WHEN dependientes BETWEEN 0 AND 0 THEN 1
      WHEN dependientes BETWEEN 1 AND 2 THEN 2
      WHEN dependientes BETWEEN 3 AND 3 THEN 3
      WHEN dependientes BETWEEN 4 AND 13 THEN 4
      ELSE NULL
    END AS cuartil
  FROM
    `riesgo-relativo-proyecto-3.super_cajaTwo.super_cajaGeneral`
)
, DatosConLimitesDependientes AS (
  SELECT
    dc.dependientes,
    dc.estado_mora,
    dc.cuartil,
    CASE
      WHEN cuartil = 1 THEN 'Cuartil 1 (Sin Dependientes)'
      WHEN cuartil = 2 THEN 'Cuartil 2 (1 a 2 Dependientes)'
      WHEN cuartil = 3 THEN 'Cuartil 3 (3 Dependientes)'
      WHEN cuartil = 4 THEN 'Cuartil 4 (4 a 13 Dependientes)'
      ELSE 'Fuera de Rango'
    END AS dependientes_cuartil
  FROM
    DatosConCuartiles dc
)
, IncidenciaExpuesto AS (
  SELECT
    cuartil,
    COUNT(*) AS casos_expuesto,
    COUNT(DISTINCT dependientes) AS poblacion_expuesto
  FROM
    DatosConLimitesDependientes
  WHERE
    estado_mora = 1 
  GROUP BY
    cuartil
)
, IncidenciaNoExpuesto AS (
  SELECT
    cuartil,
    COUNT(*) AS casos_no_expuesto,
    COUNT(DISTINCT dependientes) AS poblacion_no_expuesto
  FROM
    DatosConLimitesDependientes
  WHERE
    estado_mora = 0 
  GROUP BY
    cuartil
)
SELECT
  dcl.cuartil,
  dcl.dependientes_cuartil,
  COUNTIF(dcl.estado_mora = 0) AS dependientes_buenos_pagadores,
  COUNTIF(dcl.estado_mora = 1) AS dependientes_malos_pagadores,
  SUM(ie.casos_expuesto) AS dependientes_casos_expuesto, 
  SUM(ine.casos_no_expuesto) AS dependientes_casos_no_expuesto, 
  (SUM(ie.casos_expuesto) * 1.0 / SUM(ie.poblacion_expuesto)) / (SUM(ine.casos_no_expuesto) * 1.0 / SUM(ine.poblacion_no_expuesto)) AS dependientes_riesgo_relativo
FROM
  DatosConLimitesDependientes dcl
LEFT JOIN
  IncidenciaExpuesto ie ON dcl.cuartil = ie.cuartil
LEFT JOIN
  IncidenciaNoExpuesto ine ON dcl.cuartil = ine.cuartil
WHERE
  dcl.cuartil IS NOT NULL
GROUP BY
  dcl.cuartil, dcl.Dependientes_cuartil
ORDER BY
  dcl.cuartil;
```

<figure><img src="../../../.gitbook/assets/image (168).png" alt=""><figcaption></figcaption></figure>

### Resultado del Estudio

#### **Cuartil 1 (Sin Dependientes):**

* **Buenos Pagadores:** 20,575
* **Malos Pagadores:** 337
* **Total de Casos Expuestos:** 7,047,344
* **Total de Casos No Expuestos:** 430,264,400
* **Riesgo Relativo:** 0.0164

### Observación

En este grupo sin dependientes (Cuartil 1), el riesgo relativo es bajo (0.0164), indicando que hay una probabilidad baja de ser un mal pagador en comparación con los no expuestos.

**Cuartil 2 (1 a 2 Dependientes):**

* **Buenos Pagadores:** 10,676
* **Malos Pagadores:** 239
* **Total de Casos Expuestos:** 2,608,685
* **Total de Casos No Expuestos:** 116,528,540
* **Riesgo Relativo:** 0.0224

### Observación

En este grupo con 1 a 2 dependientes (Cuartil 2), el riesgo relativo es moderadamente bajo (0.0224), indicando que hay una probabilidad moderada baja de ser un mal pagador en comparación con los no expuestos.

**Cuartil 3 (3 Dependientes):**

* **Buenos Pagadores:** 2,260
* **Malos Pagadores:** 65
* **Total de Casos Expuestos:** 151,125
* **Total de Casos No Expuestos:** 5,254,500
* **Riesgo Relativo:** 0.0288

### Observación

En este grupo con 3 dependientes (Cuartil 3), el riesgo relativo es moderadamente alto (0.0288), indicando que hay una probabilidad moderada alta de ser un mal pagador en comparación con los no expuestos.

**Cuartil 4 (4 a 13 Dependientes):**

* **Buenos Pagadores:** 873
* **Malos Pagadores:** 32
* **Total de Casos Expuestos:** 28,960
* **Total de Casos No Expuestos:** 790,065
* **Riesgo Relativo:** 0.0733

### Observación

En este grupo con 4 a 13 dependientes (Cuartil 4), el riesgo relativo es alto (0.0733), indicando que hay una probabilidad alta de ser un mal pagador en comparación con los no expuestos.

### Conclusiones

Se realizó una comparación del riesgo relativo de ser un mal pagador en diferentes grupos según la cantidad de dependientes. El riesgo relativo varía en cada cuartil, indicando cómo el número de dependientes afecta la probabilidad de ser un mal pagador en comparación con los no expuestos.

\



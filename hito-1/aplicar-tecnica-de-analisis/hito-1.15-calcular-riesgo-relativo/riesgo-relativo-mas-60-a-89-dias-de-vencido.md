# Riesgo Relativo Más 60 a 89 días de Vencido

```sql
WITH DatosConCuartiles AS (
  SELECT
    mas60_89dias_vencido,
    estado_mora,
    CASE
      WHEN mas60_89dias_vencido BETWEEN 0 AND 0 THEN 1
      WHEN mas60_89dias_vencido BETWEEN 1 AND 1 THEN 2
      WHEN mas60_89dias_vencido BETWEEN 2 AND 3 THEN 3
      WHEN mas60_89dias_vencido BETWEEN 4 AND 98 THEN 4
      ELSE NULL
    END AS cuartil
  FROM
    `riesgo-relativo-proyecto-3.super_cajaTwo.super_cajaGeneral`
)
, DatosConLimites60mora AS (
  SELECT
    dc.mas60_89dias_vencido,
    dc.estado_mora,
    dc.cuartil,
    CASE
      WHEN cuartil = 1 THEN 'Cuartil 1 (Sin días de mora)'
      WHEN cuartil = 2 THEN 'Cuartil 2 (1 día de mora)'
      WHEN cuartil = 3 THEN 'Cuartil 3 (2 a 3 días de mora)'
      WHEN cuartil = 4 THEN 'Cuartil 4 (4 a 98 días de mora)'
      ELSE 'Fuera de Rango'
    END AS nombre_cuartil
  FROM
    DatosConCuartiles dc
)
, IncidenciaExpuesto AS (
  SELECT
    cuartil,
    COUNT(*) AS casos_expuesto,
    COUNT(DISTINCT mas60_89dias_vencido) AS poblacion_expuesto
  FROM
    DatosConLimites60mora
  WHERE
    estado_mora = 1 
  GROUP BY
    cuartil
)
, IncidenciaNoExpuesto AS (
  SELECT
    cuartil,
    COUNT(*) AS casos_no_expuesto,
    COUNT(DISTINCT mas60_89dias_vencido) AS poblacion_no_expuesto
  FROM
    DatosConLimites60mora
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
  DatosConLimites60mora dcl
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

<figure><img src="../../../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

### **Resultado de Estudio**

**Cuartil 1 (Sin días de mora):**

* **Buenos Pagadores:** 33,987
* **Malos Pagadores:** 148
* **Total de Casos Expuestos:** 5,051,980
* **Total de Casos No Expuestos:** 1,160,146,245
* **Riesgo Relativo:** 0.0044

### Observación

En este grupo donde no hay días de mora (Cuartil 1), el riesgo relativo es muy bajo (0.0044), indicando que hay una probabilidad muy baja de ser un mal pagador en comparación con los no expuestos.

**Cuartil 2 (1 día de mora):**

* **Buenos Pagadores:** 1,105
* **Malos Pagadores:** 305
* **Total de Casos Expuestos:** 430,050
* **Total de Casos No Expuestos:** 1,558,050
* **Riesgo Relativo:** 0.2760

### Observación

En este grupo con 1 día de mora (Cuartil 2), el riesgo relativo es más alto (0.2760), indicando que hay aproximadamente 0.28 veces más riesgo relativo de ser un mal pagador en comparación con los no expuestos.

**Cuartil 3 (2 a 3 días de mora):**

* **Buenos Pagadores:** 196
* **Malos Pagadores:** 150
* **Total de Casos Expuestos:** 51,900
* **Total de Casos No Expuestos:** 67,816
* **Riesgo Relativo:** 0.7653

### Observación

En este grupo con 2 a 3 días de mora (Cuartil 3), el riesgo relativo es más alto (0.7653), indicando que hay aproximadamente 0.77 veces más riesgo relativo de ser un mal pagador en comparación con los no expuestos.

**Cuartil 4 (4 a 98 días de mora):**

* **Buenos Pagadores:** 29
* **Malos Pagadores:** 80
* **Total de Casos Expuestos:** 8,720
* **Total de Casos No Expuestos:** 3,161
* **Riesgo Relativo:** 2.7586

### Observación

En este grupo con 4 a 98 días de mora (Cuartil 4), el riesgo relativo es significativamente más alto (2.7586), indicando que hay aproximadamente 2.76 veces más riesgo relativo de ser un mal pagador en comparación con los no expuestos.

### Conclusiones

Se realizó una comparación del riesgo relativo de ser un mal pagador en diferentes grupos según el número de días de mora. El riesgo relativo varía en cada cuartil, indicando cómo el rango de días de mora afecta la probabilidad de ser un mal pagador en comparación con los no expuestos.

# Riesgo Relativo Más 90 días de Vencido

```sql
WITH DatosConCuartiles AS (
  SELECT
    mas90_dias_vencido,
    estado_mora,
    CASE
      WHEN mas90_dias_vencido BETWEEN 0 AND 0 THEN 1
      WHEN mas90_dias_vencido BETWEEN 1 AND 1 THEN 2
      WHEN mas90_dias_vencido BETWEEN 2 AND 2 THEN 3
      WHEN mas90_dias_vencido BETWEEN 3 AND 98 THEN 4
      ELSE NULL
    END AS cuartil
  FROM
    `riesgo-relativo-proyecto-3.super_cajaTwo.super_cajaGeneral`
)
, DatosConLimites90mora AS (
  SELECT
    dc.mas90_dias_vencido,
    dc.estado_mora,
    dc.cuartil,
    CASE
      WHEN cuartil = 1 THEN 'Cuartil 1 (Sin días de mora)'
      WHEN cuartil = 2 THEN 'Cuartil 2 (1 día de mora)'
      WHEN cuartil = 3 THEN 'Cuartil 3 (2 días de mora)'
      WHEN cuartil = 4 THEN 'Cuartil 4 (3 a 98 días de mora)'
      ELSE 'Fuera de Rango'
    END AS mas90_cuartil
  FROM
    DatosConCuartiles dc
)
, IncidenciaExpuesto AS (
  SELECT
    cuartil,
    COUNT(*) AS casos_expuesto,
    COUNT(DISTINCT mas90_dias_vencido) AS poblacion_expuesto
  FROM
    DatosConLimites90mora
  WHERE
    estado_mora = 1 
  GROUP BY
    cuartil
)
, IncidenciaNoExpuesto AS (
  SELECT
    cuartil,
    COUNT(*) AS casos_no_expuesto,
    COUNT(DISTINCT mas90_dias_vencido) AS poblacion_no_expuesto
  FROM
    DatosConLimites90mora
  WHERE
    estado_mora = 0 
  GROUP BY
    cuartil
)
SELECT
  dcl.cuartil,
  dcl.mas90_cuartil,
  COUNTIF(dcl.estado_mora = 0) AS mas90_buenos_pagadores,
  COUNTIF(dcl.estado_mora = 1) AS mas90_malos_pagadores,
  SUM(ie.casos_expuesto) AS mas90_casos_expuesto, 
  SUM(ine.casos_no_expuesto) AS mas90_casos_no_expuesto, 
  (SUM(ie.casos_expuesto) * 1.0 / SUM(ie.poblacion_expuesto)) / (SUM(ine.casos_no_expuesto) * 1.0 / SUM(ine.poblacion_no_expuesto)) AS mas90_riesgo_relativo
FROM
  DatosConLimites90mora dcl
LEFT JOIN
  IncidenciaExpuesto ie ON dcl.cuartil = ie.cuartil
LEFT JOIN
  IncidenciaNoExpuesto ine ON dcl.cuartil = ine.cuartil
WHERE
  dcl.cuartil IS NOT NULL
GROUP BY
  dcl.cuartil, dcl.mas90_cuartil
ORDER BY
  dcl.cuartil;
```

<figure><img src="../../../.gitbook/assets/image (171).png" alt=""><figcaption></figcaption></figure>

### Resulatdo de Estudio

**Cuartil 1 (Sin días de mora):**

* **Buenos Pagadores:** 33,998
* **Malos Pagadores:** 56
* **Total de Casos Expuestos:** 1,907,024
* **Total de Casos No Expuestos:** 1,157,767,892
* **Riesgo Relativo:** 0.00165

### Observación

En este grupo sin días de mora (Cuartil 1), el 0.165% de los casos expuestos son malos pagadores en comparación con los no expuestos. Este cuartil muestra un riesgo relativo muy bajo.

**Cuartil 2 (1 día de mora):**

* **Buenos Pagadores:** 1,006
* **Malos Pagadores:** 214
* **Total de Casos Expuestos:** 261,080
* **Total de Casos No Expuestos:** 1,227,320
* **Riesgo Relativo:** 0.2127

### Observación

En este grupo con 1 día de mora (Cuartil 2), el 21.27% de los casos expuestos son malos pagadores en comparación con los no expuestos. Este cuartil muestra un riesgo relativo moderadamente alto.

**Cuartil 3 (2 días de mora):**

* **Buenos Pagadores:** 196
* **Malos Pagadores:** 159
* **Total de Casos Expuestos:** 56,445
* **Total de Casos No Expuestos:** 69,580
* **Riesgo Relativo:** 0.8112

### Observación

En este grupo con 2 días de mora (Cuartil 3), el 81.12% de los casos expuestos son malos pagadores en comparación con los no expuestos. Este cuartil muestra un riesgo relativo alto.

**Cuartil 4 (3 a 98 días de mora):**

* **Buenos Pagadores:** 117
* **Malos Pagadores:** 254
* **Total de Casos Expuestos:** 94,234
* **Total de Casos No Expuestos:** 43,407
* **Riesgo Relativo:** 1.7057

### Observación

En este grupo con 3 a 98 días de mora (Cuartil 4), el 170.57% de los casos expuestos son malos pagadores en comparación con los no expuestos. Este cuartil muestra el riesgo relativo más alto.

### Conclusiones

Se realizó una comparación del riesgo relativo de ser un mal pagador en diferentes grupos según el número de días de mora. A medida que avanzas de un cuartil a otro, se observa un aumento significativo en el riesgo relativo, indicando que los grupos con más días de mora tienen proporciones más altas de malos pagadores en comparación con los no expuestos.

\

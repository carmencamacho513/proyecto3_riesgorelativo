# Riesgo Relativo ultimo\_salario

```sql
WITH DatosConCuartiles AS (
  SELECT
    ultimo_salario,
    estado_mora,
    CASE
      WHEN ultimo_salario BETWEEN 0 AND 3707 THEN 1
      WHEN ultimo_salario BETWEEN 3708 AND 6261 THEN 2
      WHEN ultimo_salario BETWEEN 6262 AND 9717 THEN 3
      WHEN ultimo_salario BETWEEN 9718 AND 1560100 THEN 4
      ELSE NULL
    END AS cuartil
  FROM
    `riesgo-relativo-proyecto-3.super_cajaTwo.super_cajaGeneral`
)
, DatosConLimitesSalario AS (
  SELECT
    dc.ultimo_salario,
    dc.estado_mora,
    dc.cuartil,
   CASE
      WHEN cuartil = 1 THEN 'Cuartil 1 (0-3707 USD Mensual)'
      WHEN cuartil = 2 THEN 'Cuartil 2 (3708-6261 USD Mensual)'
      WHEN cuartil = 3 THEN 'Cuartil 3 (6262-9717 USD Mensual)'
      WHEN cuartil = 4 THEN 'Cuartil 4 (9718-1560100 USD Mensual)'
      ELSE 'Fuera de Rango'
    END AS salario_cuartil
  FROM
    DatosConCuartiles dc
)
, IncidenciaExpuesto AS (
  SELECT
    cuartil,
    COUNT(*) AS casos_expuesto,
    COUNT(DISTINCT ultimo_salario) AS poblacion_expuesto
  FROM
    DatosConLimitesSalario
  WHERE
    estado_mora = 1 
  GROUP BY
    cuartil
)
, IncidenciaNoExpuesto AS (
  SELECT
    cuartil,
    COUNT(*) AS casos_no_expuesto,
    COUNT(DISTINCT ultimo_salario) AS poblacion_no_expuesto
  FROM
    DatosConLimitesSalario
  WHERE
    estado_mora = 0 
  GROUP BY
    cuartil
)
SELECT
  dcl.cuartil,
  dcl.salario_cuartil,
  COUNTIF(dcl.estado_mora = 0) AS salario_buenos_pagadores,
  COUNTIF(dcl.estado_mora = 1) AS salario_malos_pagadores,
  SUM(ie.casos_expuesto) AS salario_casos_expuesto, 
  SUM(ine.casos_no_expuesto) AS salario_casos_no_expuesto, 
  (SUM(ie.casos_expuesto) * 1.0 / SUM(ie.poblacion_expuesto)) / (SUM(ine.casos_no_expuesto) * 1.0 / SUM(ine.poblacion_no_expuesto)) AS salario_riesgo_relativo
FROM
  DatosConLimitesSalario dcl
LEFT JOIN
  IncidenciaExpuesto ie ON dcl.cuartil = ie.cuartil
LEFT JOIN
  IncidenciaNoExpuesto ine ON dcl.cuartil = ine.cuartil
WHERE
  dcl.cuartil IS NOT NULL
GROUP BY
  dcl.cuartil, dcl.salario_cuartil
ORDER BY
  dcl.cuartil;
```

<figure><img src="../../../.gitbook/assets/image (170).png" alt=""><figcaption></figcaption></figure>

### Resultado del Estudio

**Cuartil 1 (0-3707 USD Mensual):**

* **Buenos Pagadores:** 8,112
* **Malos Pagadores:** 246
* **Total de Casos Expuestos:** 2,056,068
* **Total de Casos No Expuestos:** 67,800,096
* **Riesgo Relativo:** 0.3929

### Observación

En este grupo con ingresos mensuales entre 0 y 3707 USD (Cuartil 1), el 39.29% de los casos expuestos son malos pagadores en comparación con los no expuestos. Este cuartil muestra un riesgo relativo alto.

**Cuartil 2 (3708-6261 USD Mensual):**

* **Buenos Pagadores:** 8,589
* **Malos Pagadores:** 188
* **Total de Casos Expuestos:** 1,650,076
* **Total de Casos No Expuestos:** 75,385,653
* **Riesgo Relativo:** 0.3485

### Observación

&#x20;En este grupo con ingresos mensuales entre 3708 y 6261 USD (Cuartil 2), el 34.85% de los casos expuestos son malos pagadores en comparación con los no expuestos. Este cuartil muestra un riesgo relativo alto.

**Cuartil 3 (6262-9717 USD Mensual):**

* **Buenos Pagadores:** 6,617
* **Malos Pagadores:** 90
* **Total de Casos Expuestos:** 603,630
* **Total de Casos No Expuestos:** 44,380,219
* **Riesgo Relativo:** 0.3277

### Observación

En este grupo con ingresos mensuales entre 6262 y 9717 USD (Cuartil 3), el 32.77% de los casos expuestos son malos pagadores en comparación con los no expuestos. Este cuartil muestra un riesgo relativo alto.

**Cuartil 4 (9718-1560100 USD Mensual):**

* **Buenos Pagadores:** 4,930
* **Malos Pagadores:** 29
* **Total de Casos Expuestos:** 143,811
* **Total de Casos No Expuestos:** 24,447,870
* **Riesgo Relativo:** 0.4

### Observación

En este grupo con ingresos mensuales entre 9718 y 1,560,100 USD (Cuartil 4), el 40% de los casos expuestos son malos pagadores en comparación con los no expuestos. Este cuartil muestra un riesgo relativo alto.

### Conclusiones

Se realiza una comparación del riesgo relativo de ser un mal pagador en diferentes grupos según el rango de ingresos mensuales. Los cuartiles 1, 2 y 4 muestran riesgos relativos elevados, indicando que los grupos con ingresos específicos tienen proporciones más altas de malos pagadores en comparación con los no expuestos.

\

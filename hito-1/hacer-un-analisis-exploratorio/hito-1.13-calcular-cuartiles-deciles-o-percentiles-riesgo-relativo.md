# Hito 1.13 Calcular cuartiles, deciles o percentiles (Riesgo Relativo)

## Meta

Calcular cuartiles, deciles o percentiles

## Objetivo

Calcular cuartiles para las variables del riesgo relativo en BigQuery

Se realizo el calculo de cuartiles y la medida de riesgo relativo para cada variable en estudio.

```sql
WITH DatosConCuartiles AS (
  SELECT
    edad,
    estado_mora,
    NTILE(4) OVER (ORDER BY edad) AS cuartil
  FROM
    `riesgo-relativo-proyecto-3.super_cajaTwo.super_cajaGeneral`
)
, DatosConLimitesEdad AS (
  SELECT
    dc.edad,
    dc.estado_mora,
    dc.cuartil,
   CASE
      WHEN cuartil = 1 THEN 'Cuartil 1 (Adulto)'
      WHEN cuartil = 2 THEN 'Cuartil 2 (Adulto Medio)'
      WHEN cuartil = 3 THEN 'Cuartil 3 (Adulto Mayor)'
      WHEN cuartil = 4 THEN 'Cuartil 4 (Fuera de los Parámetros)'
      ELSE 'Fuera de Rango'
    END AS nombre_cuartil
  FROM
    DatosConCuartiles dc
)
, IncidenciaExpuesto AS (
  SELECT
    cuartil,
    COUNT(*) AS casos_expuesto,
    COUNT(DISTINCT edad) AS poblacion_expuesto
  FROM
    DatosConLimitesEdad
  WHERE
    estado_mora = 1 
  GROUP BY
    cuartil
)
, IncidenciaNoExpuesto AS (
  SELECT
    cuartil,
    COUNT(*) AS casos_no_expuesto,
    COUNT(DISTINCT edad) AS poblacion_no_expuesto
  FROM
    DatosConLimitesEdad
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
  DatosConLimitesEdad dcl
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

<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

### **Resultado del Estudio**

#### **Cuartil 1 (Adulto)**

* **Buenos Pagadores:** 8,692
* **Malos Pagadores:** 308
* **Total de Casos Expuestos:** 2,781,000
* **Total de Casos No Expuestos:** 78,201,000
* **Riesgo Relativo:** 0.0393

### **Observación**

En este grupo de adultos (Cuartil 1), el 3.93% de los casos expuestos son malos pagadores en comparación con los no expuestos. Este cuartil muestra un riesgo relativo más alto.

#### **Cuartil 2 (Adulto Medio)**

* **Buenos Pagadores:** 8,797
* **Malos Pagadores:** 203
* **Total de Casos Expuestos:** 1,827,000
* **Total de Casos No Expuestos:** 79,182,000
* **Riesgo Relativo:** 0.0231

### **Observación**

En este grupo de adultos medios (Cuartil 2), el 2.31% de los casos expuestos son malos pagadores en comparación con los no expuestos. Este cuartil muestra un riesgo relativo más bajo que el Cuartil 1.

#### **Cuartil 3 (Adulto Mayor)**

* **Buenos Pagadores:** 8,879
* **Malos Pagadores:** 121
* **Total de Casos Expuestos:** 1,089,000
* **Total de Casos No Expuestos:** 79,920,000
* **Riesgo Relativo:** 0.0136

### Observación

En este grupo de adultos mayores (Cuartil 3), el 1.36% de los casos expuestos son malos pagadores en comparación con los no expuestos. Este cuartil muestra un riesgo relativo más bajo.

#### **Cuartil 4 (Fuera de los Parámetros)**

* **Buenos Pagadores:** 8,949
* **Malos Pagadores:** 51
* **Total de Casos Expuestos:** 450,000
* **Total de Casos No Expuestos:** 80,550,000
* **Riesgo Relativo:** 0.0109

### Observación

En este grupo fuera de los parámetros (Cuartil 4), el 1.09% de los casos expuestos son malos pagadores en comparación con los no expuestos. Este cuartil muestra el riesgo relativo más bajo.

## Conclusiones

Se realiza una comparación del riesgo relativo de ser un mal pagador en diferentes grupos según la clasificación en cuartiles. A medida que avanzas de un cuartil a otro, se observa una disminución en el riesgo relativo, indicando que los grupos con características específicas (en este caso, Adulto, Adulto Medio, Adulto Mayor y Fuera de los Parámetros) tienen diferentes proporciones de malos pagadores en comparación con los no expuestos.

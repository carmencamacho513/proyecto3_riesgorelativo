# Riesgo Relativo Edad

```sql
WITH DatosConCuartiles AS (
  SELECT
    edad,
    estado_mora,
    CASE
      WHEN edad BETWEEN 21 AND 39 THEN 1
      WHEN edad BETWEEN 40 AND 58 THEN 2
      WHEN edad BETWEEN 59 AND 75 THEN 3
      WHEN edad BETWEEN 76 AND 109 THEN 4
      ELSE NULL
    END AS cuartil
  FROM
    `riesgo-relativo-proyecto-3.super_cajaTwo.super_cajaGeneral`
)
, DatosConLimitesEdad AS (
  SELECT
    dc.edad,
    dc.estado_mora,
    dc.cuartil,
   CASE
      WHEN cuartil = 1 THEN 'Cuartil 1 (Edad de 21 a 39 años)'
      WHEN cuartil = 2 THEN 'Cuartil 2 (Edad de 40 a 58 años)'
      WHEN cuartil = 3 THEN 'Cuartil 3 (Edad de 59 a 75 años)'
      WHEN cuartil = 4 THEN 'Cuartil 4 (Edad de 76 a 109 años)'
      ELSE 'Fuera de Rango'
    END AS edad_cuartil
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
  dcl.edad_cuartil,
  COUNTIF(dcl.estado_mora = 0) AS edad_buenos_pagadores,
  COUNTIF(dcl.estado_mora = 1) AS edad_malos_pagadores,
  SUM(ie.casos_expuesto) AS edad_casos_expuesto, 
  SUM(ine.casos_no_expuesto) AS edad_casos_no_expuesto, 
  (SUM(ie.casos_expuesto) * 1.0 / SUM(ie.poblacion_expuesto)) / (SUM(ine.casos_no_expuesto) * 1.0 / SUM(ine.poblacion_no_expuesto)) AS edad_riesgo_relativo
FROM
  DatosConLimitesEdad dcl
LEFT JOIN
  IncidenciaExpuesto ie ON dcl.cuartil = ie.cuartil
LEFT JOIN
  IncidenciaNoExpuesto ine ON dcl.cuartil = ine.cuartil
WHERE
  dcl.cuartil IS NOT NULL
GROUP BY
  dcl.cuartil, dcl.edad_cuartil
ORDER BY
  dcl.cuartil;
```

<figure><img src="../../../.gitbook/assets/image (169).png" alt=""><figcaption></figcaption></figure>

### Resultado del Estudio

#### **Cuartil 1 (Edad de 21 a 39 años):**

* **Buenos Pagadores:** 7,309
* **Malos Pagadores:** 268
* **Total de Casos Expuestos:** 2,030,636
* **Total de Casos No Expuestos:** 55,380,293
* **Riesgo Relativo:** 0.0410

### **Observación**

En este grupo de personas con edades entre 21 y 39 años (Cuartil 1), el 4.10% de los casos expuestos son malos pagadores en comparación con los no expuestos. Este cuartil muestra un riesgo relativo más alto.

**Cuartil 2 (Edad de 40 a 58 años):**

* **Buenos Pagadores:** 15,612
* **Malos Pagadores:** 332
* **Total de Casos Expuestos:** 5,293,408
* **Total de Casos No Expuestos:** 248,917,728
* **Riesgo Relativo:** 0.0213

### Observación

&#x20;En este grupo de personas con edades entre 40 y 58 años (Cuartil 2), el 2.13% de los casos expuestos son malos pagadores en comparación con los no expuestos. Este cuartil muestra un riesgo relativo más bajo que el Cuartil 1.

**Cuartil 3 (Edad de 59 a 75 años):**

* **Buenos Pagadores:** 9,907
* **Malos Pagadores:** 72
* **Total de Casos Expuestos:** 718,488
* **Total de Casos No Expuestos:** 98,861,953
* **Riesgo Relativo:** 0.00772

### Observación

&#x20;En este grupo de personas con edades entre 59 y 75 años (Cuartil 3), el 0.772% de los casos expuestos son malos pagadores en comparación con los no expuestos. Este cuartil muestra un riesgo relativo aún más bajo.

**Cuartil 4 (Edad de 76 a 109 años):**

* **Buenos Pagadores:** 2,489
* **Malos Pagadores:** 11
* **Total de Casos Expuestos:** 27,500
* **Total de Casos No Expuestos:** 6,222,500
* **Riesgo Relativo:** 0.0144

### Observación

&#x20;En este grupo de personas con edades entre 76 y 109 años (Cuartil 4), el 1.44% de los casos expuestos son malos pagadores en comparación con los no expuestos. Este cuartil muestra un riesgo relativo más bajo que el Cuartil 1.

### Conclusiones

Se realiza una comparación del riesgo relativo de ser un mal pagador en diferentes grupos según el rango de edad. A medida que se avanza de un cuartil a otro, se observa una variación en el riesgo relativo, indicando que los grupos de diferentes edades tienen diferentes proporciones de malos pagadores en comparación con los no expuestos. El Cuartil 1, con edades de 21 a 39 años, muestra el riesgo relativo más alto en este conjunto de datos.

\


##

##

##


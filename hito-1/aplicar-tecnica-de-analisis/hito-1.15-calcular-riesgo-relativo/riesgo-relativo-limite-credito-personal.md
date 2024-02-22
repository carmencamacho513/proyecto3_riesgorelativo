# Riesgo Relativo Limite Credito Personal

##

```sql
WITH DatosConCuartiles AS (
  SELECT
    limite_credito_personal,
    estado_mora,
    CASE
      WHEN limite_credito_personal BETWEEN 0 AND 0.029520998 THEN 1
      WHEN limite_credito_personal BETWEEN 0.029528177 AND 0.149653131  THEN 2
      WHEN limite_credito_personal BETWEEN 0.14965669 AND 0.548523682  THEN 3
      WHEN limite_credito_personal BETWEEN 0.548545145 AND 22000  THEN 4
      ELSE NULL
    END AS cuartil
  FROM
    `riesgo-relativo-proyecto-3.super_cajaTwo.super_cajaGeneral`
)
, DatosConLimitesCredito AS (
  SELECT
    dc.limite_credito_personal,
    dc.estado_mora,
    dc.cuartil,
     CASE
      WHEN cuartil = 1 THEN 'Cuartil 1 (0 a 0.029520998 Total Bienes)'
      WHEN cuartil = 2 THEN 'Cuartil 2 (0.029528177 a 0.149653131 Total Bienes)'
      WHEN cuartil = 3 THEN 'Cuartil 3 (0.14965669 a 0.548523682 Total Bienes)'
      WHEN cuartil = 4 THEN 'Cuartil 4 (0.548545145 a 22000 Total Bienes)'
      ELSE 'Fuera de Rango'
    END AS limite_cuartil
  FROM
    DatosConCuartiles dc
)
, IncidenciaExpuesto AS (
  SELECT
    cuartil,
    COUNT(*) AS casos_expuesto,
    COUNT(DISTINCT limite_credito_personal) AS poblacion_expuesto
  FROM
    DatosConLimitesCredito
  WHERE
    estado_mora = 1 
  GROUP BY
    cuartil
)
, IncidenciaNoExpuesto AS (
  SELECT
    cuartil,
    COUNT(*) AS casos_no_expuesto,
    COUNT(DISTINCT limite_credito_personal) AS poblacion_no_expuesto
  FROM
    DatosConLimitesCredito
  WHERE
    estado_mora = 0 
  GROUP BY
    cuartil
)
SELECT
  dcl.cuartil,
  dcl.limite_cuartil,
  COUNTIF(dcl.estado_mora = 0) AS limite_buenos_pagadores,
  COUNTIF(dcl.estado_mora = 1) AS limite_malos_pagadores,
  SUM(ie.casos_expuesto) AS limite_casos_expuesto, 
  SUM(ine.casos_no_expuesto) AS limite_casos_no_expuesto, 
  (SUM(ie.casos_expuesto) * 1.0 / SUM(ie.poblacion_expuesto)) / (SUM(ine.casos_no_expuesto) * 1.0 / SUM(ine.poblacion_no_expuesto)) AS limite_riesgo_relativo
FROM
  DatosConLimitesCredito dcl
LEFT JOIN
  IncidenciaExpuesto ie ON dcl.cuartil = ie.cuartil
LEFT JOIN
  IncidenciaNoExpuesto ine ON dcl.cuartil = ine.cuartil
WHERE
  dcl.cuartil IS NOT NULL
GROUP BY
  dcl.cuartil, dcl.limite_cuartil
ORDER BY
  dcl.cuartil;  
```

<figure><img src="../../../.gitbook/assets/image (174).png" alt=""><figcaption></figcaption></figure>

### **Resultado de Estudio**

**Cuartil 1 (0 a 0.029520998 Total Bienes):**

* **Buenos Pagadores:** 8,992
* **Malos Pagadores:** 8
* **Total de Casos Expuestos:** 72,000
* **Total de Casos No Expuestos:** 80,928,000
* **Riesgo Relativo:** 2.8132

### Observación

En este grupo con un rango bajo de Total Bienes (Cuartil 1), el 2.8132 indica que hay aproximadamente 2.81 veces más riesgo relativo de ser un mal pagador en comparación con los no expuestos.

**Cuartil 2 (0.029528177 a 0.149653131 Total Bienes):**

* **Buenos Pagadores:** 8,999
* **Malos Pagadores:** 1
* **Total de Casos Expuestos:** 9,000
* **Total de Casos No Expuestos:** 80,991,000
* **Riesgo Relativo:** 0.9958

### Observación

En este grupo con un rango medio de Total Bienes (Cuartil 2), el 0.9958 indica que no hay un riesgo significativo adicional de ser un mal pagador en comparación con los no expuestos.

**Cuartil 3 (0.14965669 a 0.548523682 Total Bienes):**

* **Buenos Pagadores:** 8,966
* **Malos Pagadores:** 34
* **Total de Casos Expuestos:** 306,000
* **Total de Casos No Expuestos:** 80,694,000
* **Riesgo Relativo:** 0.9971

### Observación

En este grupo con un rango medio-alto de Total Bienes (Cuartil 3), el 0.9971 indica que no hay un riesgo significativo adicional de ser un mal pagador en comparación con los no expuestos.

**Cuartil 4 (0.548545145 a 22000 Total Bienes):**

* **Buenos Pagadores:** 8,360
* **Malos Pagadores:** 640
* **Total de Casos Expuestos:** 5,760,000
* **Total de Casos No Expuestos:** 75,240,000
* **Riesgo Relativo:** 1.0517

### Observación

En este grupo con un rango alto de Total Bienes (Cuartil 4), el 1.0517 indica que hay aproximadamente 1.05 veces más riesgo relativo de ser un mal pagador en comparación con los no expuestos.

### Conclusiones

Se realizó una comparación del riesgo relativo de ser un mal pagador en diferentes grupos según el valor total de bienes. El riesgo relativo varía en cada cuartil, indicando cómo el rango de valor de bienes afecta la probabilidad de ser un mal pagador en comparación con los no expuestos.

\

# Hito 2.1 Nuevas Variables Dummys.

## Meta

Crear nuevas variables

## Objetivo

Crear variables dummies para calculo del score

```sql
SELECT
  user_id,
  estado_mora,
  CASE
    WHEN edad BETWEEN 21 AND 39 THEN 1
    WHEN edad BETWEEN 40 AND 58 THEN 2
    WHEN edad BETWEEN 59 AND 75 THEN 3
    WHEN edad BETWEEN 76 AND 109 THEN 4
    ELSE NULL
  END AS cuartil_edad,
  CASE
    WHEN dependientes BETWEEN 0 AND 0 THEN 1
    WHEN dependientes BETWEEN 1 AND 2 THEN 2
    WHEN dependientes BETWEEN 3 AND 3 THEN 3
    WHEN dependientes BETWEEN 4 AND 13 THEN 4
    ELSE NULL
  END AS cuartil_dependientes,
  CASE
    WHEN limite_credito_personal BETWEEN 0 AND 0.029520998 THEN 1
    WHEN limite_credito_personal BETWEEN 0.029528177 AND 0.149653131 THEN 2
    WHEN limite_credito_personal BETWEEN 0.14965669 AND 0.548523682 THEN 3
    WHEN limite_credito_personal BETWEEN 0.548545145 AND 22000 THEN 4
    ELSE NULL
  END AS cuartil_credito,
  CASE
    WHEN mas90_dias_vencido BETWEEN 0 AND 0 THEN 1
    WHEN mas90_dias_vencido BETWEEN 1 AND 1 THEN 2
    WHEN mas90_dias_vencido BETWEEN 2 AND 2 THEN 3
    WHEN mas90_dias_vencido BETWEEN 3 AND 98 THEN 4
    ELSE NULL
  END AS cuartil_mas90,
  CASE
    WHEN ratio_deuda BETWEEN 0 AND 0.195110482 THEN 1
    WHEN ratio_deuda BETWEEN 0.195140307 AND 0.382692908 THEN 2
    WHEN ratio_deuda BETWEEN 0.382700903 AND 0.968784838 THEN 3
    WHEN ratio_deuda BETWEEN 0.97009911 AND 307001 THEN 4
    ELSE NULL
  END AS cuartil_ratio,
  CASE
    WHEN ultimo_salario BETWEEN 0 AND 3707 THEN 1
    WHEN ultimo_salario BETWEEN 3708 AND 6261 THEN 2
    WHEN ultimo_salario BETWEEN 6262 AND 9717 THEN 3
    WHEN ultimo_salario BETWEEN 9718 AND 1560100 THEN 4
    ELSE NULL
  END AS cuartil_salario
FROM
  `riesgo-relativo-proyecto-3.super_cajaTwo.super_cajaGeneral`;



```

```sql
SELECT
    user_id,
    estado_mora,
    IF(cuartil_edad IN (2, 3, 4), 1, 0) AS dummy_edad,  
    IF(cuartil_dependientes IN (1, 2, 3), 1, 0) AS dummy_dependientes,
    IF(cuartil_credito IN (2, 3, 4), 1, 0) AS dummy_credito,
    IF(cuartil_mas90 IN (1, 2, 3), 1, 0) AS dummy_mas90,
    IF(cuartil_ratio IN (2, 3, 4), 1, 0) AS dummy_ratio,
    IF(cuartil_salario IN (1, 2, 3), 1, 0) AS dummy_salario
  FROM
    `riesgo-relativo-proyecto-3.super_cajaTwo.cuartil_dummys`
```

### Conclusiones

Se utiliza los cuartiles que se utilizó para hacer el riesgo relativo y a base de estos resultados realizamos las nuevas variables Dummies.



### OPRIME <mark style="color:red;">En conceptos Obtenidos en el Proceso</mark> encuentras la definición de variables Dummies:

{% content-ref url="../../conceptos-obtenidos-en-el-proceso..md" %}
[conceptos-obtenidos-en-el-proceso..md](../../conceptos-obtenidos-en-el-proceso..md)
{% endcontent-ref %}

###

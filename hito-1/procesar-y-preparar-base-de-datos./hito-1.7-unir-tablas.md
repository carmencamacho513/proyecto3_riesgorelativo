# Hito 1.7 Unir Tablas

## Meta

Unir tablas.

## Objetivo

Entender el comando JOIN y sus variedades para juntar tablas distintas.

```sql
SELECT
  *
FROM
  `riesgo-relativo-proyecto-3.super_cajaOne.viewOne_cajaTwo`
FULL JOIN
  `riesgo-relativo-proyecto-3.super_cajaThree.view_cajaThree`
USING
  (user_id)
FULL JOIN
  `riesgo-relativo-proyecto-3.super_cajaFour.cajaFour_view`
USING
  (user_id)
```

## Conclusiones

Se realiza la unión de las tablas con FULL JOIN muestra toda la información de ambas tablas, y si no hay coincidencias en alguna fila, se rellena con valores nulos.&#x20;

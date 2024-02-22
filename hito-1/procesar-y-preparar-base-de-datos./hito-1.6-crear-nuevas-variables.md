# Hito 1.6 Crear Nuevas Variables

## Meta

Crear nuevas variables.

## Objetivo

Construir nuevas variables y guardar en una nueva tabla o view.

```sql
SELECT
    user_id,
    SUM(CASE WHEN tipo_prestamo = 'real estate' THEN 1 ELSE 0 END) AS real_bienes,
    SUM(CASE WHEN tipo_prestamo = 'other' THEN 1 ELSE 0 END) AS otros_prestamos
FROM
    `riesgo-relativo-proyecto-3.super_cajaFour.cajaFour_uno`
GROUP BY
    user_id;
```

<figure><img src="../../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>

```sql
SELECT
CORR(real_bienes, otros_prestamos) AS correlation,
AVG(real_bienes) AS AVG_real,
AVG(otros_prestamos) AS AVG_otros
FROM
  `riesgo-relativo-proyecto-3.super_cajaFour.cajaFour_view`
```

<figure><img src="../../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

## Conclusiones

Se realizó las dos nuevas variables real\_bienes y otros\_prestamos y se calculo la correlación de estas dando como resultado una correlación positiva,  sugiere que cuando una variable aumenta, la otra tiende a aumentar también, y viceversa. Sin embargo, la fuerza de esta relación es moderada, ya que el valor está por encima de cero pero no es muy alto.

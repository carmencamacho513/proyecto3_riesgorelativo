# Hito 1.5 Variables Categóricas - Cambiar Tipo de Dato

## Meta

Identificar y manejar datos inconsistentes en variables categóricas.

Comprobar y cambiar tipo de dato.

## Objetivo

Identificar y tratar los valores inconsistentes utilizando comandos SQL, como [UPPER](https://cloud.google.com/bigquery/docs/reference/standard-sql/string\_functions#upper), [LOWER](https://cloud.google.com/bigquery/docs/reference/standard-sql/string\_functions#lower).

Utilizar en algún momento del proyecto CAST, SAFE\_CAST o otro comando en SQL para alterar el formato de una variable.



```sql
SELECT
 loan_type
FROM
  `riesgo-relativo-proyecto-3.super_cajaFour.prestamos_pendientes`
WHERE
  loan_type <> 'real estate'
```

<figure><img src="../../.gitbook/assets/image (130).png" alt=""><figcaption></figcaption></figure>

```sql
SELECT
  loan_type
FROM
 `riesgo-relativo-proyecto-3.super_cajaFour.prestamos_pendientes`
WHERE
  loan_type <> 'other'
```

<figure><img src="../../.gitbook/assets/image (107).png" alt=""><figcaption></figcaption></figure>

```sql
SELECT
  * EXCEPT(loan_type, loan_id),
  loan_id AS id_prestamo,
  CASE
    WHEN loan_type = 'others' THEN 'other'
  ELSE
  LOWER(loan_type)
END
  AS tipo_prestamo,
FROM
  `riesgo-relativo-proyecto-3.super_cajaFour.prestamos_pendientes`
```

## Conclusiones

Se realizo la sentencia con <> para buscar que palabras estaban diferentes y luego se utilizó en el caso (CASE), cuando (WHEN) se encuentre la palabra 'others' pasar (THE) 'other' y las demás (ELSE) en minúsculas (LOWER). Tambien se realiza cambio en el nombre de las variables.

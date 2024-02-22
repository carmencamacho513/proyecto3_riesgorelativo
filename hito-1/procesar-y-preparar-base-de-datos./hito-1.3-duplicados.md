# Hito 1.3 Duplicados

## Meta

Identificar y manejar valores duplicados

## Objetivo

Identificar duplicados a través de comandos SQL COUNT, GROUP BY, HAVING

```sql
SELECT
  loan_type, COUNT (*) AS cantidad_double
FROM
  `scenic-lane-408815.two_listBox.loans_ outstanding`
GROUP BY
  loan_type
HAVING
  COUNT(*) > 1
```

<figure><img src="../../.gitbook/assets/image (114).png" alt=""><figcaption></figcaption></figure>

## Conclusiones

Se realizaron la búsqueda de duplicados en las 4 tablas.

No se encontraron duplicados.

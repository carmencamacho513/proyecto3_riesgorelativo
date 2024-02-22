# Unión de las Tablas

```sql
SELECT
  *
FROM
  `riesgo-relativo-proyecto-3.super_cajaOne.info_usuario`
LEFT JOIN
  `riesgo-relativo-proyecto-3.super_cajaTwo.por_defecto` 
USING
  (user_id)
```

```sql
SELECT
  COUNTIF(default_flag = 1
    AND last_month_salary IS NULL) AS unos_nulos,
  COUNTIF(default_flag = 0
    AND last_month_salary IS NULL) AS cero_nulos
FROM
  `riesgo-relativo-proyecto-3.super_cajaOne.unionOne_cajaTwo`
```

<figure><img src="../../../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

### Conclusiones

Se encontraro 130 nulos donde el cliente es moroso y 7064 nulos donde el cliente es buen pagador.

# Hito 1.2 Valores Nulos

## Meta

Identificar y manejar valores nulos.

## Objetivo

Identificar nulos a través de comandos SQL COUNT, WHERE y IS NULL.

**riesgo-relativo-proyecto-3.super\_cajaOne.info\_usuario**

```sql
SELECT
  COUNT(user_id) AS user_id,
  COUNT(age) AS age,
  COUNT(sex) AS sex,
  COUNT(last_month_salary) AS last_month_salary,
  COUNT(number_dependents) AS number_dependents
FROM
  `riesgo-relativo-proyecto-3.super_cajaOne.info_usuario`
WHERE
  user_id IS NOT NULL
  OR age IS NOT NULL
  OR sex IS NOT NULL
  OR last_month_salary IS NOT NULL
  OR number_dependents IS NOT NULL
```

<figure><img src="../../../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

### Conclusiones

En esta tabla hay 36.000 filas de las cuales la variable **ultimo\_salario** tiene **7199** **nulos** y la variable **dependientes** tiene **943 nulos**.

**riesgo-relativo-proyecto-3.super\_cajaTwo.por\_defecto**

```sql
SELECT
COUNT(user_id),
COUNT(default_flag)
FROM
  `riesgo-relativo-proyecto-3.super_cajaTwo.por_defecto`
WHERE
user_id IS NOT NULL
OR default_flag IS NOT NULL
```

<figure><img src="../../../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

### Conclusiones

En esta tabla no hay nulos.

**riesgo-relativo-proyecto-3.super\_cajaThree.prestamos\_detalles**

```sql
SELECT
  COUNT(user_id),
  COUNT(more_90_days_overdue),
  COUNT(using_lines_not_secured_personal_assets),
  COUNT(number_times_delayed_payment_loan_30_59_days),
  COUNT(debt_ratio),
  COUNT(number_times_delayed_payment_loan_60_89_days),
FROM
  `riesgo-relativo-proyecto-3.super_cajaThree.prestamos_detalles`
WHERE
  user_id IS NOT NULL
  OR more_90_days_overdue IS NOT NULL
  OR using_lines_not_secured_personal_assets IS NOT NULL
  OR number_times_delayed_payment_loan_30_59_days IS NOT NULL
  OR debt_ratio IS NOT NULL
  OR number_times_delayed_payment_loan_60_89_days IS NOT NULL

```

<figure><img src="../../../.gitbook/assets/image (126).png" alt=""><figcaption></figcaption></figure>

### Conclusiones

No se encontraron nulos en esta tabla hay 36000 filas.

**riesgo-relativo-proyecto-3.super\_cajaFour.prestamos\_pendientes**

```sql
SELECT
COUNT(loan_id),
COUNT(user_id),
COUNT(loan_type)
FROM
  `riesgo-relativo-proyecto-3.super_cajaFour.prestamos_pendientes`
WHERE
loan_id IS NOT NULL
OR user_id IS NOT NULL
OR loan_type IS NOT NULL
```

<figure><img src="../../../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

### Conclusiones

No hay nulos en esta tabla.

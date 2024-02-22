# Hito 1.4 Datos Fuera del alcance (Correlación)

## Meta

Identificar y manejar datos fuera del alcance del análisis.

## Objetivo

Utilizar CORR para comprender la correlación entre variables.

**riesgo-relativo-proyecto-3.super\_cajaOne.unionOne\_cajaTwo**

```sql
SELECT
  CORR(more_90_days_overdue, number_times_delayed_payment_loan_30_59_days) AS correlation_loan30,
  CORR(more_90_days_overdue, number_times_delayed_payment_loan_60_89_days) AS correlation_loan60,
  CORR(number_times_delayed_payment_loan_30_59_days, number_times_delayed_payment_loan_60_89_days) AS correlation_loan90
FROM
  `riesgo-relativo-proyecto-3.super_cajaThree.prestamos_detalles`
```

<figure><img src="../../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

## Medidas&#x20;

```sql
SELECT
  AVG(number_times_delayed_payment_loan_30_59_days) AS AVG_days30,
  APPROX_QUANTILES(number_times_delayed_payment_loan_30_59_days, 2)[
OFFSET
  (1)] AS mediana_days30,
  MIN(number_times_delayed_payment_loan_30_59_days) AS min_days30,
  MAX(number_times_delayed_payment_loan_30_59_days) AS max_days30,
  STDDEV(number_times_delayed_payment_loan_30_59_days) AS stddev_days30,
  AVG(number_times_delayed_payment_loan_60_89_days) AS AVG_days60,
  APPROX_QUANTILES(number_times_delayed_payment_loan_60_89_days, 2)[
OFFSET
  (1)] AS mediana_days60,
  MIN(number_times_delayed_payment_loan_60_89_days) AS min_days60,
  MAX(number_times_delayed_payment_loan_60_89_days) AS max_days60,
  STDDEV(number_times_delayed_payment_loan_60_89_days) AS stddev_days60,
  AVG(more_90_days_overdue) AS AVG_days90,
  APPROX_QUANTILES(more_90_days_overdue, 2)[
OFFSET
  (1)] AS mediana_days90,
  MIN(more_90_days_overdue) AS min_days90,
  MAX(more_90_days_overdue) AS max_days90,
  STDDEV(more_90_days_overdue) AS stddev_days90
FROM
  `scenic-lane-408815.three_listBox.loans_detail`
```

<figure><img src="../../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>

```sql
SELECT
  *EXCEPT(more_90_days_overdue, using_lines_not_secured_personal_assets, number_times_delayed_payment_loan_30_59_days, debt_ratio, number_times_delayed_payment_loan_60_89_days),
  more_90_days_overdue AS mas90_dias_vencido,
  using_lines_not_secured_personal_assets AS limite_credito_personal,
  debt_ratio AS ratio_deuda,
  number_times_delayed_payment_loan_60_89_days AS mas60_89dias_vencido
FROM
  `riesgo-relativo-proyecto-3.super_cajaThree.prestamos_detalles`
```

## Conclusiones

Se realizo la correlación y desviación estándar de las siguientes variables: number\_times\_delayed\_payment\_loan\_30\_59\_days, number\_times\_delayed\_payment\_loan\_60\_89\_days y more\_90\_days\_overdue y tomando en cuenta la siguiente descripción: analizando los coeficientes de desviación estándar, podemos identificar cuál de las dos variables con alta correlación tiene una desviación mayor, lo que la hace más representativa y más interesante para el análisis, por lo que excluimos la variable con menor desviación.

Por lo anterior tome la decisión de seguir trabajando con la variable como principal more\_90\_days\_overdue y entre las variables number\_times\_delayed\_payment\_loan\_30\_59\_days y number\_times\_delayed\_payment\_loan\_60\_89\_days; la opción de la última; ya que tiene una desviación estándar de 4.105514755101970, que es menor en comparación con la primera y la tercera. Sin embargo, la correlación de esta variable es muy alta, con un valor de 0.992175526340. Esto la hace más representativa y más interesante para el análisis, según el criterio de seleccionar la variable con alta correlación y desviación estándar mayor.

Por lo tanto utilice SELECT EXEPT para excluir la variable y hacer el cambio el nombre de las otras variables.

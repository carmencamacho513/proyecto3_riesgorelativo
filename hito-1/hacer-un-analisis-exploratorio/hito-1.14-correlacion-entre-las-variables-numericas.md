# Hito 1.14 Correlación entre las Variables Numéricas

## Meta

Calcular correlación entre las variables numéricas

## Objetivo

Entender la relación que existe entre las variables numéricas usando correlaciones. Utiliza gráficos de dispersión y línea de tendencia. Puedes utilizar también el comando CORR en Bigquery

```sql
SELECT
  CORR(ultimo_salario, mas90_dias_vencido) AS correlation_mas90,
  CORR(ultimo_salario, ratio_deuda) AS correlation_ratio
FROM
  `riesgo-relativo-proyecto-3.super_cajaTwo.super_cajaGeneral`
```

<figure><img src="../../.gitbook/assets/image (96).png" alt=""><figcaption></figcaption></figure>



<figure><img src="../../.gitbook/assets/image (100).png" alt=""><figcaption></figcaption></figure>

### OPRIME <mark style="color:red;">Google Colaboratory</mark> Encuentra el proceso.

{% embed url="https://colab.research.google.com/drive/1Hf683p2CbfKSHN6Cps_SBhGzDM_e2iZi?usp=sharing" %}

## Conclusiones

* **1:** Existe una correlación positiva perfecta, lo que significa que cuando una variable aumenta, la otra también lo hace de manera proporcional.
* **0:** No hay correlación, las variables no están relacionadas.
* **-1:** Existe una correlación negativa perfecta, lo que significa que cuando una variable aumenta, la otra disminuye de manera proporcional.

En tu caso, los resultados de correlación son:

1. **Correlación entre estado\_mora y edad: -0.0624**
   * Interpretación: Hay una correlación negativa muy débil (-0.0624) entre el estado de mora y la edad. Esto sugiere que, en general, no hay una relación fuerte entre la edad y el estado de mora.
2. **Correlación entre estado\_mora y ultimo\_salario: -0.0206**
   * Interpretación: Hay una correlación negativa muy débil (-0.0206) entre el estado de mora y el último salario. Esto sugiere que, en general, no hay una relación fuerte entre el último salario y el estado de mora.
3. **Correlación entre estado\_mora y dependientes: 0.0372**
   * Interpretación: Hay una correlación positiva muy débil (0.0372) entre el estado de mora y la cantidad de dependientes. Esto sugiere que, en general, no hay una relación fuerte entre la cantidad de dependientes y el estado de mora.
4. **Correlación entre estado\_mora y mas90\_dias\_vencido: 0.4133**
   * Interpretación: Hay una correlación positiva moderada (0.4133) entre el estado de mora y la variable mas90\_dias\_vencido. Esto sugiere que hay una relación más fuerte entre el retraso de más de 90 días en los pagos y el estado de mora.
5. **Correlación entre estado\_mora y limite\_credito\_personal: -0.0025**
   * Interpretación: Hay una correlación negativa muy débil (-0.0025) entre el estado de mora y el límite de crédito personal. Esto sugiere que, en general, no hay una relación fuerte entre el límite de crédito personal y el estado de mora.
6. **Correlación entre estado\_mora y ratio\_deuda: -0.0020**
   * Interpretación: Hay una correlación negativa muy débil (-0.0020) entre el estado de mora y la proporción de deuda. Esto sugiere que, en general, no hay una relación fuerte entre la proporción de deuda y el estado de mora.
7. **Correlación entre estado\_mora y mas60\_89dias\_vencido: 0.2729**
   * Interpretación: Hay una correlación positiva moderada (0.2729) entre el estado de mora y la variable mas60\_89dias\_vencido. Esto sugiere que hay una relación más fuerte entre el retraso de 60 a 89 días en los pagos y el estado de mora.
8. **Correlación entre estado\_mora y real\_bienes: -0.0243**
   * Interpretación: Hay una correlación negativa muy débil (-0.0243) entre el estado de mora y la variable real\_bienes. Esto sugiere que, en general, no hay una relación fuerte entre la propiedad de bienes y el estado de mora.
9. **Correlación entre estado\_mora y otros\_prestamos: -0.0431**
   * Interpretación: Hay una correlación negativa débil (-0.0431) entre el estado de mora y la variable otros\_prestamos. Esto sugiere que, en general, no hay una relación fuerte entre otros préstamos y el estado de mora.

En resumen, en la mayoría de los casos, las correlaciones son débiles, lo que indica que estas variables no están fuertemente relacionadas entre sí. Sin embargo, es importante considerar el contexto específico de tu análisis y la naturaleza de tus datos para una interpretación más completa.

\

# Hito 3.1 Variable Dummies en Google Colab

## Meta

conectar/importar datos a otras herramientas

Crear nuevas variables

## Objetivo

Crear un nuevo Google Colab e importar tablas para realizar el hito 2

Transformar variables categóricas en variables numéricas

### OPRIME <mark style="color:red;">Google Colaboraty</mark> encuentras el Proceso.

{% embed url="https://colab.research.google.com/drive/12a4h89E1lInxIFgPQ7Gv9HZ5hHFQLvxj?usp=sharing" %}

### Variable Dummy

```python
df.info()
```

<figure><img src="../../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

```notebook-python
tipo_genero = pd.get_dummies(df['genero'], prefix='genero')
tipo_genero.head()
```

<figure><img src="../../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

```notebook-python
tipo_genero = pd.get_dummies(df['genero'], prefix='genero', drop_first=True)
tipo_genero.head()
```

<figure><img src="../../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

```notebook-python
df = pd.concat([df, tipo_genero], axis=1)
df = df.drop('genero', axis=1)
print(df)
```

<figure><img src="../../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

```notebook-python
df.info()
```

<figure><img src="../../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

#### Conclusiones

Se realiza importación de datos y para la transformación de la variable categórica **'genero'**  en variable numérica se utiliza las variable dummies.

#### Definición:&#x20;

Una variable dummy es una variable binaria (0 o 1) que se utiliza para representar categorías o grupos. Supongamos que tienes una variable categórica con dos categorías, por ejemplo, "A" y "B". Para incluir esta variable en un modelo de regresión o clasificación, puedes crear una variable dummy que tome el valor 0 cuando la categoría es "A" y 1 cuando es "B".

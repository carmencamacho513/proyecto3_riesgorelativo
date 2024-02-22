# Imputación de Datos utilizando paquete SkitLearn

### OPRIME <mark style="color:red;">Google Colaboraty</mark> encuentras el Proceso.

{% embed url="https://colab.research.google.com/drive/1EnL20HAM1OJ0Z2cJB4CGmw4MM-k1mrPQ?usp=sharing" %}



```python
df.info()
```

<figure><img src="../../../.gitbook/assets/image (176).png" alt=""><figcaption></figcaption></figure>

```python
scaler = MinMaxScaler()
df = pd.DataFrame(scaler.fit_transform(df), columns = df.columns)
df.head()
```

<figure><img src="../../../.gitbook/assets/image (177).png" alt=""><figcaption></figcaption></figure>

```python
imputer = KNNImputer(n_neighbors=5)
df = pd.DataFrame(imputer.fit_transform(df), columns = df.columns)
```

```notebook-python
df.info()
```

<figure><img src="../../../.gitbook/assets/image (178).png" alt=""><figcaption></figcaption></figure>

```notebook-python
df.head()
```

<figure><img src="../../../.gitbook/assets/image (179).png" alt=""><figcaption></figcaption></figure>








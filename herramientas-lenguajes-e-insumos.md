# 💸 Herramientas, lenguajes e insumos

### 1.1 Herramientas y/o plataformas <a href="#id-11herramientasyoplataformas" id="id-11herramientasyoplataformas"></a>

En este proyecto vas a utilizar cuatro herramientas de Google, una para el manejo de los datos en SQL, una para crear presentaciones, una otra para la visualización del resultado de tu trabajo y la última para manejo de datos en Python:

* Google BigQuery: Almacén de datos que permite el procesamiento de grandes volúmenes de datos.
* Google Colab: Plataforma para trabajar con Python en Notebooks
* Google Slides: Herramienta para la creación y edición de presentaciones.
* Google Looker Studio: Herramienta para la creación y edición de dashboards, informes de datos.

### 1.2 Lenguajes <a href="#id-12lenguajes" id="id-12lenguajes"></a>

Utilizarás el lenguaje SQL en BigQuery y Python en Google Colab.

### 1.3 Insumos <a href="#id-13insumos" id="id-13insumos"></a>

Este conjunto de datos contiene datos sobre préstamos concedidos a un grupo de clientes del Bacon. Los datos se dividen en 4 tablas, la primera con datos del usuario/cliente, la segunda con datos del tipo de préstamo, la tercera con el comportamiento de pago de estos préstamos, y la cuarta con la identificación de clientes ya identificados como morosos.

El conjunto de datos está disponible para download en este enlace [dataset](https://drive.google.com/file/d/1BbQHMdlIVh\_wQrjFp50qa2036ai2CA-W/view?usp=sharing), ten en cuenta que es un archivo comprimido, tendrás que descomprimirlo para acceder a los archivos con los datos.

A continuación, puedes consultar la descripción de las variables que componen las tablas de este conjunto de datos:

| Archivo             | Variable                                                   | Descripción                                                                                                                                                     |
| ------------------- | ---------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| user\_ info         | user\_ id                                                  | Número de identificación del cliente (único para cada cliente)                                                                                                  |
|                     | age                                                        | Edad del cliente                                                                                                                                                |
|                     | sex                                                        | Sexo del cliente                                                                                                                                                |
|                     | last\_ month\_ salary                                      | Último salario mensual que el cliente reportó al banco                                                                                                          |
|                     | number\_dependents                                         | Número de dependientes                                                                                                                                          |
| loans\_ outstanding | loan\_ id                                                  | Número de identificación del préstamo (único para cada préstamo)                                                                                                |
|                     | user\_ id                                                  | Número de identificación del cliente                                                                                                                            |
|                     | loan\_ type                                                | Tipo de préstamo (real estate = inmobiliario, others = otro)                                                                                                    |
| loans\_ detail      | user\_ id                                                  | Número de identificación del cliente                                                                                                                            |
|                     | more\_ 90\_ days\_ overdue                                 | Número de veces que el cliente estuvo más de 90 días vencido                                                                                                    |
|                     | using\_ lines\_ not\_ secured\_ personal\_ assets          | Cuánto está utilizando el cliente en relación con su límite de crédito, en líneas que no están garantizadas con bienes personales, como inmuebles y automóviles |
|                     | number\_ times\_ delayed\_ payment\_ loan\_ 30\_ 59\_ days | Número de veces que el cliente se retrasó en el pago de un préstamo (entre 30 y 59 días)                                                                        |
|                     | debt\_ ratio                                               | Relación entre las deudas y el patrimonio del prestatario. ratio de deuda = Deudas / Patrimonio                                                                 |
|                     | number\_ times\_ delayed\_ payment\_ loan\_ 60\_ 89\_ days | Número de veces que el cliente retrasó el pago de un préstamo, (entre 60 y 89 días)                                                                             |
| default             | user\_ id                                                  | Número de identificación del cliente                                                                                                                            |
|                     | default\_ flag                                             | Clasificación de los clientes morosos (1 para clientes que pagan mal, 0 para clientes que pagan bien)                                                           |


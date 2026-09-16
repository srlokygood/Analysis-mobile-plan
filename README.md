# 📊 Análisis de uso de clientes de telecomunicaciones

## 🎯 Objetivo del proyecto

El objetivo de este proyecto es realizar un **análisis exploratorio del comportamiento de los clientes del servicio de telecomunicaciones de telecomm**, utilizando información demográfica y registros de llamadas y mensajes y tipos de plan.

El análisis busca comprender los patrones de uso de los clientes, identificar posibles problemas de calidad en los datos y segmentar a los usuarios según su edad y nivel de uso de llamadas y mensajes.

---

## 📂 Datasets utilizados

El proyecto utiliza dos conjuntos de datos principales:

### `users`

Contiene información relacionada con los clientes:

* `user_id`: identificador único del cliente.
* `age`: edad del cliente.
* `city`: ciudad de residencia.
* `plan`: plan contratado.
* `reg_date`: fecha de registro.
* `churn_date`: fecha de cancelación del servicio.

### `usage`

Contiene los registros de uso del servicio:

* `id`: identificador del registro.
* `user_id`: identificador del cliente.
* `type`: tipo de comunicación (`call` o `text`).
* `duration`: duración de las llamadas.
* `length`: cantidad de caracteres de los mensajes.
* `date`: fecha del registro de uso.

### `plans`

Contiene los diferentes planes:

* `plan_name `: identificador del plan.
* `messages_included`: caracteristicas del paquete, mensajes incluidos.
* `gb_per_month`: caracteristicas del paquete, gibaytes incluidos por mes.
* `minutes_included`: caracteristicas del paquete, minutos incluidos.
* `usd_monthly_pay`: cantidad de caracteres de los mensajes.
* `usd_per_gb`: costo dolares por gb.
* `usd_per_message`: costo dolares por mensaje.
* `usd_per_minute`: costo dolares por minuto.


---

## 🔎 Etapas del análisis

### 1. Exploración inicial de los datos

Se realizó una revisión inicial de las tablas para:

* Identificar los tipos de datos de cada columna.
* Analizar la estructura y dimensiones de los datasets.
* Revisar valores nulos.
* Identificar valores únicos y posibles inconsistencias.
* Comprender la relación entre las tablas mediante `user_id`.

### 2. Limpieza y preparación de los datos

Durante esta etapa se identificaron y trataron diferentes problemas de calidad:

* Las columnas `reg_date` y `date` fueron tratadas como variables de tipo fecha.
* Se identificó el valor centinela `-999` en `age` y se reemplazó utilizando el promedio estadístico de la columna.
* Los valores `?` encontrados en `city` fueron reemplazados por valores nulos.
* Se verificaron fechas posteriores a la fecha actual para identificar posibles fechas imposibles. No se encontraron registros que requirieran modificación.

También se analizaron los valores nulos de `duration` y `length` en relación con `type`, identificando que estos valores están relacionados con el tipo de registro:

* Los registros `call` deben contener información de `duration`.
* Los registros `text` deben contener información de `length`.

Los valores inesperados fueron convertidos a `NaN`.

### 3. Análisis estadístico

Se calcularon estadísticas descriptivas para variables como:

* Edad.
* Cantidad de mensajes.
* Cantidad de llamadas.
* Minutos acumulados de llamadas.
* Longitud total de mensajes.

Se analizaron medidas como:

* Media.
* Desviación estándar.
* Mínimo y máximo.
* Cuartiles.
* Mediana.

También se utilizaron histogramas y boxplots para observar la distribución de los datos e identificar posibles valores atípicos.

### 4. Agregación de información

Los registros de uso fueron agrupados por `user_id` para obtener información acumulada por cliente:

* `cant_mensajes`: cantidad total de mensajes.
* `cant_llamadas`: cantidad total de llamadas.
* `cant_minutos_llamada`: duración total de las llamadas.
* `longitud_mensajes_total`: cantidad total de caracteres enviados mediante mensajes.

Posteriormente, esta información fue integrada con la tabla `users`.

### 5. Análisis de distribuciones y valores atípicos

Se analizaron las distribuciones de las principales variables mediante histogramas y boxplots.

Entre los principales hallazgos:

* La edad presenta clientes principalmente entre los 30 y 60 años.
* La cantidad de mensajes presenta un sesgo hacia la derecha, con mayor concentración en cantidades bajas de mensajes.
* La cantidad de llamadas presenta una distribución cercana a una campana, con un ligero sesgo hacia la derecha.
* La duración de las llamadas presenta un sesgo hacia la derecha, concentrándose la mayoría de los registros en duraciones bajas.
* La longitud total de mensajes presenta valores atípicos elevados, llegando hasta aproximadamente 2.000 caracteres.

Los valores atípicos fueron evaluados considerando que un valor extremo no necesariamente representa un error. Cuando no existía evidencia suficiente para considerarlos incorrectos, se conservaron para no perder información sobre los clientes con mayor nivel de uso.

### 6. Segmentación de clientes

Se realizaron dos segmentaciones principales.

#### 👥 Segmentación por edad

Los clientes fueron agrupados en:

| Segmento        |      Rango de edad |
| --------------- | -----------------: |
| Jóvenes         | Menores de 30 años |
| Adultos         |       30 a 60 años |
| Adultos mayores | Mayores de 60 años |

El grupo con mayor representación corresponde a los clientes entre 30 y 60 años.

#### 📊 Segmentación por nivel de uso

Los clientes fueron clasificados según su cantidad de mensajes y llamadas:

| Segmento  | Criterio                         |
| --------- | -------------------------------- |
| Bajo uso  | Menos de 5 mensajes o llamadas   |
| Uso medio | Entre 5 y 10 mensajes o llamadas |
| Alto uso  | Más de 10 mensajes o llamadas    |

El segmento predominante corresponde al **uso medio**, seguido por el grupo de bajo uso. El grupo de alto uso representa una proporción menor de los clientes.

---

## 💡 Conclusiones

Los resultados muestran que la mayoría de los clientes presenta un nivel de uso medio de llamadas y mensajes de texto. El grupo etario con mayor representación corresponde a los adultos entre 30 y 60 años.

El análisis de la cantidad total de caracteres enviados mediante mensajes permitió complementar el análisis de frecuencia de mensajes y obtener una visión más detallada del uso que realizan los clientes de este servicio.

---

## 🚀 Recomendaciones para análisis posteriores

Como continuación del análisis, se propone:

* Analizar qué tipo de plan utiliza cada grupo etario y qué nivel de uso presenta.
* Comparar el uso de llamadas y mensajes entre los diferentes grupos de edad.
* Analizar la relación entre el plan contratado y el comportamiento de uso.
* Profundizar en la cantidad de caracteres enviados por los clientes que utilizan mensajes de texto.

---

## 🛠️ Tecnologías utilizadas

* **Python**
* **Pandas** — manipulación y limpieza de datos.
* **NumPy** — tratamiento de valores nulos y operaciones numéricas.
* **Matplotlib** — visualización de datos.
* **Jupyter Notebook / Google Colab** — desarrollo y documentación del análisis.

---

## ▶️ Cómo ejecutar el proyecto

### Opción 1 — Google Colab

1. Clonar o descargar este repositorio.
2. Abrir el archivo `.ipynb`.
3. Acceder a [Google Colab](https://colab.research.google.com/).
4. Seleccionar **Archivo → Subir notebook**.
5. Cargar el notebook del proyecto.
6. Subir los datasets a la sesión de Colab o ajustar las rutas de los archivos.
7. Ejecutar las celdas en orden.

### Opción 2 — Jupyter Notebook local

1. Tener instalado Python.
2. Instalar las librerías necesarias:

```bash
pip install pandas numpy matplotlib jupyter
```

3. Clonar el repositorio:

```bash
git clone <URL_DEL_REPOSITORIO>
```

4. Acceder a la carpeta del proyecto:

```bash
cd <NOMBRE_DEL_PROYECTO>
```

5. Ejecutar Jupyter Notebook:

```bash
jupyter notebook
```

6. Abrir el archivo `.ipynb` y ejecutar las celdas en orden.

---

## 🔁 Guía de reproducción

Para reproducir el análisis completo:

1. Cargar los datasets `users` y `usage`.
2. Revisar la estructura y los tipos de datos.
3. Identificar y tratar valores nulos y centinela.
4. Formatear las variables de fecha.
5. Analizar los valores nulos de `duration` y `length` según `type`.
6. Corregir los valores inesperados.
7. Crear las variables agregadas por `user_id`.
8. Integrar la información mediante `user_id`.
9. Calcular estadísticas descriptivas.
10. Generar histogramas y boxplots.
11. Analizar y evaluar los valores atípicos.
12. Crear la segmentación por edad.
13. Crear la segmentación por nivel de uso.
14. Analizar los resultados y elaborar las conclusiones.

---

## 📌 Estructura sugerida del repositorio

```text
├── data/
│   ├── users.csv
│   └── usage.csv
│
├── notebooks/
│   └── analisis_clientes.ipynb
│
├── README.md
└── requirements.txt
```

---

## 👤 Autor

**Jair — Data Analyst en formación**

Proyecto desarrollado como parte del proceso de formación en análisis de datos.

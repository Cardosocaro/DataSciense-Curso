# Data Science – Spotify: popularidad y perfiles musicales

Repositorio de las cuatro etapas de la formación en Data Science: fundamentos con NumPy y Pandas, exploración del catálogo de Spotify, aprendizaje supervisado y clustering no supervisado.

---

## 📚 Contenido del repositorio

En este repositorio se encuentran notebooks correspondientes a las diferentes actividades prácticas realizadas durante el curso, incluyendo ejercicios de NumPy, Pandas y el desarrollo del proyecto final.

### Notebooks

- `TP1-numpy5.ipynb`
  - Ejercicios de Ciencia de Datos utilizando NumPy.
  - Aplicación sobre un conjunto de datos.

- ` TP2_Pandas_de_tarea_ventas-3.ipynb`
  - Ejercicios de análisis y manipulación de datos utilizando Pandas.
  - Trabajo sobre un conjunto de datos de ventas.

- `Tp-Final/EDA_Spotify.ipynb`: exploración, limpieza y visualización del dataset Spotify.
- `Tp-Final/Modelado_Supervisado_Spotify.ipynb`: regresión y clasificación, con validación y optimización.
- `Tp-Final/Modelado_No_Supervisado_Spotify.ipynb`: clustering K-Means, PCA e interpretación de perfiles musicales.

---

# 🎵 Proyecto Final: Análisis de canciones de Spotify

## Objetivo

El objetivo del proyecto es analizar las características musicales de diferentes canciones de Spotify para estudiar su relación con el nivel de popularidad.

La pregunta principal que orienta el análisis es:

> **¿Qué características musicales están relacionadas con la popularidad de una canción y cómo varían estas características entre los distintos géneros musicales?**

La variable `popularity` se toma como referencia para analizar el nivel de popularidad de las canciones.

Como objetivo complementario, el clustering descubre perfiles musicales sin usar popularidad ni género como etiquetas.

---

## 📊 Dataset

El proyecto utiliza un dataset de canciones de Spotify disponible en Kaggle.

El conjunto de datos contiene información sobre canciones, artistas, álbumes, géneros musicales y diferentes características de audio.

Entre las principales variables se encuentran:

- `track_id`: identificador de la canción.
- `artists`: artista o artistas.
- `album_name`: nombre del álbum.
- `track_name`: nombre de la canción.
- `popularity`: nivel de popularidad.
- `duration_ms`: duración de la canción en milisegundos.
- `explicit`: indica si la canción posee contenido explícito.
- `danceability`: medida relacionada con qué tan adecuada resulta una canción para bailar.
- `energy`: nivel de energía de la canción.
- `key`: tonalidad.
- `loudness`: volumen sonoro.
- `mode`: modalidad musical.
- `speechiness`: presencia de contenido hablado.
- `acousticness`: medida relacionada con características acústicas.
- `instrumentalness`: probabilidad de que una canción sea instrumental.
- `liveness`: presencia de características asociadas a una interpretación en vivo.
- `valence`: medida relacionada con el carácter positivo o negativo de la canción.
- `tempo`: tempo de la canción.
- `time_signature`: métrica o compás.
- `track_genre`: género musical.

Fuente del dataset:

https://www.kaggle.com/datasets/saichaitanyareddyai/spotify-tracks-dataset-audio-features

---

# 🔎 Análisis Exploratorio de Datos (EDA)

El notebook `EDA_Spotify.ipynb` contiene el análisis exploratorio correspondiente a la segunda pre-entrega del proyecto final.

## 1. Exploración inicial

Se analiza:

- Dimensión del dataset.
- Primeras filas.
- Información general.
- Tipos de datos.
- Variables numéricas y categóricas.
- Cantidad de valores únicos.
- Estadísticas descriptivas.

---

## 2. Calidad de los datos

Se verifican:

- Valores faltantes.
- Porcentaje de valores faltantes.
- Registros duplicados.

Durante la limpieza se identificaron valores faltantes en las variables:

- `artists`
- `album_name`
- `track_name`

Estos valores fueron tratados utilizando la categoría `"Desconocido"`.

También se identificaron registros duplicados, los cuales fueron eliminados para evitar que afectaran los análisis posteriores.

---

## 3. Análisis de popularidad

Se analiza la distribución de la variable `popularity` mediante:

- Estadísticas descriptivas.
- Histograma.
- Categorización de los niveles de popularidad.

Se crearon las siguientes categorías:

- Baja
- Media-Baja
- Media-Alta
- Alta

Esto permite facilitar la interpretación de la distribución de popularidad de las canciones.

---

## 4. Análisis por género musical

Se analiza la distribución de canciones entre los diferentes géneros musicales.

Además, se calcula la popularidad promedio de cada género para identificar diferencias entre las distintas categorías musicales.

---

## 5. Relación entre características musicales y popularidad

Se estudian las relaciones entre `popularity` y diferentes características de audio:

- `danceability`
- `energy`
- `valence`

Para ello se utilizan gráficos de dispersión y análisis de correlación.

---

## 6. Matriz de correlación

Se construye una matriz de correlación para analizar las relaciones lineales entre las variables numéricas.

Los resultados muestran que las características musicales individuales presentan correlaciones débiles con `popularity`.

En particular:

- `danceability`: correlación aproximadamente 0,034.
- `energy`: correlación aproximadamente 0,001.
- `valence`: correlación aproximadamente -0,041.

Esto indica que la popularidad no parece estar explicada de manera significativa por una única característica musical.

---

# 🛠️ Transformaciones realizadas

Como parte del proceso de preparación de los datos se realizaron diferentes transformaciones.

### Duración

La variable `duration_ms`, expresada en milisegundos, fue transformada creando una nueva variable:

`duration_min`

Esta variable representa la duración de cada canción en minutos y facilita su interpretación.

### Popularidad

La variable `popularity` también fue categorizada para facilitar determinados análisis exploratorios.

---

# 📌 Principales conclusiones

El análisis permitió conocer la estructura y composición del dataset y detectar diferentes aspectos relacionados con la calidad de los datos.

Se identificaron y trataron valores faltantes y registros duplicados.

La distribución de canciones entre géneros se mantiene relativamente equilibrada, lo que permite realizar comparaciones entre diferentes géneros musicales.

Respecto de la popularidad, se observa una mayor concentración de canciones en niveles bajos y medios, mientras que las canciones con niveles de popularidad altos representan una proporción menor del conjunto de datos.

Por otro lado, el análisis de correlaciones muestra que características como `danceability`, `energy` y `valence` presentan relaciones lineales débiles con la popularidad.

Esto sugiere que la popularidad de una canción no puede explicarse únicamente a partir de una característica musical individual y que podrían intervenir múltiples factores.

Los resultados obtenidos en esta etapa servirán como base para las siguientes fases del proyecto, incluyendo la selección de variables y el desarrollo de modelos predictivos.

---

# 🤖 Modelado supervisado

Se desarrollan dos problemas: regresión para estimar `popularity` y clasificación para predecir `popularity_category`. Se comparan Ridge y Random Forest en regresión (MAE, RMSE y R²), y regresión logística y Random Forest en clasificación (accuracy, balanced accuracy y Macro F1).

Las transformaciones se incluyen en pipelines para prevenir data leakage. La partición train/test y la validación cruzada agrupan por `track_id`; así, la misma canción no aparece en ambos conjuntos. La optimización usa sólo el conjunto de entrenamiento y las brechas entre entrenamiento y validación ayudan a controlar overfitting.

# 🧩 Modelado no supervisado

El notebook de clustering agrupa canciones por `danceability`, `energy`, `valence`, `acousticness`, `instrumentalness`, `speechiness`, `liveness` y `tempo`. Imputa eventuales faltantes con la mediana y estandariza todas las variables porque K-Means utiliza distancias.

Compara entre 2 y 8 clusters con el método del codo e índice silhouette y elige el valor con mejor silhouette de la grilla evaluada. PCA permite visualizar los resultados, mientras que tablas y mapas de calor describen los perfiles con sus medias reales. Los clusters son segmentos descriptivos de audio, no géneros ni causas de popularidad.

# ▶️ Instalación y ejecución

Se recomienda Python 3.10 o superior. Instalar las dependencias:

```bash
python -m pip install pandas numpy matplotlib seaborn scikit-learn jupyter
```

Abrir Jupyter desde la raíz del repositorio y ejecutar los notebooks de arriba hacia abajo. Los notebooks de `Tp-Final/` localizan automáticamente `Data/spotify-tracks-dataset-detailed.csv`, por lo que no dependen de una ruta de Google Colab ni de otro notebook ejecutado previamente. La secuencia sugerida es: fundamentos, EDA, modelado supervisado y clustering.

Limitaciones: K-Means favorece grupos compactos, los resultados dependen de las variables seleccionadas y PCA simplifica la información al graficar dos componentes.

---


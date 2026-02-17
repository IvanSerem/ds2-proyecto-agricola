# 🌾 DS2 – Proyecto Agrícola  
## Contextualización Climática del Rendimiento Agrícola en Argentina (2014–2023)

https://github.com/IvanSerem/ds2-proyecto-agricola/blob/main/DCII_IvanSeremczuk_PrimeraEntrega.py

Proyecto desarrollado para la cursada de **Data Science II**, enfocado en el análisis de eventos climáticos reales y su posible impacto en el rendimiento agrícola provincial.

---

# 📌 1. Abstracto

En la primera etapa del proyecto (Data Science I) se construyó un modelo predictivo agrícola capaz de estimar el rendimiento de cultivos a partir de variables de suelo y clima, alcanzando métricas de alto desempeño (R² ≈ 0.97).

En esta segunda etapa, el enfoque evoluciona hacia la comprensión del contexto climático real en el que esos rendimientos ocurren.

El objetivo es analizar datos climáticos oficiales de Argentina (2014–2023) para identificar patrones provinciales, estructuras temporales de precipitación y perfiles climáticos diferenciados que puedan influir en la estabilidad productiva.

Este análisis puede resultar útil para:
- Productores agrícolas
- Analistas del sector agroindustrial
- Profesionales en planificación productiva
- Estudiantes de ciencia de datos aplicada al agro

---

# 📊 2. Resumen de Metadata

Fuente: API oficial **NASA POWER**

Características del dataset:
- 83.996 registros diarios
- 23 provincias argentinas
- Período: 2014–2023
- Variables analizadas:
  - Temperatura media diaria (T2M)
  - Precipitación diaria (PRECTOTCORR)
  - Velocidad del viento (WS2M)
  - Humedad relativa (RH2M)

Tipo de variables:
- Numéricas continuas
- Datos diarios agregados posteriormente a nivel provincial

---

# ❓ 3. Preguntas / Hipótesis de Investigación

## Temperatura
- ¿Cuáles son las provincias con mayor temperatura media anual?
- ¿Existe relación entre temperatura media anual y precipitación total?

## Precipitación
- ¿Qué provincias presentan mayor precipitación acumulada?
- ¿Cómo se distribuye la precipitación diaria?
- ¿La lluvia se concentra en eventos intensos o se distribuye de forma uniforme?
- ¿Qué provincias presentan mayor cantidad de rachas de lluvia?
- ¿Cuál es la frecuencia de días sin precipitaciones?

## Humedad
- ¿Cuáles son las provincias con mayor humedad relativa promedio?
- ¿Existe relación entre humedad y precipitación anual?

## Viento
- ¿Qué provincias presentan mayor porcentaje de días con viento intenso?

## Análisis Multivariable
- ¿Existen agrupamientos naturales de provincias según su comportamiento climático?
- ¿Qué relaciones estructurales se observan entre temperatura, precipitación, viento y humedad?

---

# 📈 4. Análisis Realizado

- Limpieza y transformación de datos
- Análisis exploratorio (EDA)
- Distribución de variables climáticas
- Estudio de rachas de lluvia
- Análisis de correlación
- Clustering climático provincial (KMeans)
- Visualizaciones interactivas y comparativas

---

# 🔎 5. Insights Principales

- El territorio argentino presenta perfiles climáticos diferenciados a nivel provincial.
- La estructura temporal de la lluvia (frecuencia y rachas) es más relevante productivamente que el acumulado anual.
- Se identificaron agrupamientos naturales de provincias con características climáticas similares.
- Las diferencias regionales pueden influir en la estabilidad del rendimiento agrícola incluso bajo condiciones de suelo favorables.

---

# ⚙️ 6. Reproducibilidad

El proyecto puede ejecutarse en:

- Google Colab
- Kaggle
- Entorno local Python 3.x

Dependencias principales:
- pandas
- numpy
- matplotlib
- seaborn
- plotly
- scikit-learn
- requests

---

# 👤 Autor

Iván Seremczuk - Comisión 77750 - Data Science II - Coderhouse 2026  



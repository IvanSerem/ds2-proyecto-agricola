# DS2 – Proyecto Agrícola  
## Análisis Climático y Contextualización del Rendimiento Agrícola en Argentina (2014–2023)

## 📌 Descripción

Este proyecto forma parte de la cursada de Data Science II y tiene como objetivo analizar datos climáticos reales de Argentina para comprender su posible impacto en el rendimiento agrícola.

En la etapa anterior (Data Science I), se desarrolló un modelo predictivo agrícola con alto desempeño (R² ≈ 0.97) utilizando variables de suelo y clima.  
En esta segunda etapa, el enfoque se orienta a estudiar el comportamiento climático real por provincia y su estructura temporal.

---

## 🎯 Objetivo

Analizar eventos climáticos ocurridos en Argentina entre 2014 y 2023 y detectar patrones provinciales relevantes para el contexto productivo agrícola.

---

## 🌎 Fuente de Datos

- API oficial NASA POWER
- 83.996 registros diarios
- 23 provincias
- Período: 2014–2023
- Variables analizadas:
  - Temperatura media (T2M)
  - Precipitación (PRECTOTCORR)
  - Velocidad del viento (WS2M)
  - Humedad relativa (RH2M)

---

## 📊 Análisis Realizado

- Análisis univariado y bivariado
- Distribución de precipitación diaria
- Frecuencia de días sin lluvia
- Estudio de rachas de lluvia
- Análisis de correlaciones
- Clustering climático provincial (KMeans)
- Visualizaciones interactivas

---

## 🔍 Principales Hallazgos

- Existen perfiles climáticos diferenciados entre provincias.
- La estructura temporal de la lluvia (rachas) es más relevante productivamente que el acumulado anual.
- Se identificaron agrupamientos naturales de provincias con características climáticas similares.
- La variabilidad climática provincial puede influir en la estabilidad del rendimiento agrícola.

---

## ⚙️ Reproducibilidad

El notebook puede ejecutarse en:
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

## 👤 Autor

Iván Serem  
Proyecto académico – Data Science II

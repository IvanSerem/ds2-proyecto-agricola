# 🌾 DS2 – Proyecto Agrícola  
## Contextualización Climática y Modelado Predictivo de Precipitación en Argentina (2014–2023)

Proyecto desarrollado para la cursada de **Data Science II** en **Coderhouse**, enfocado en el análisis de datos climáticos reales de Argentina y en la construcción de un modelo de **Machine Learning** capaz de estimar la precipitación a partir de variables meteorológicas, geográficas y temporales.

🔗 **Demo interactiva en Hugging Face Spaces:**  
https://huggingface.co/spaces/IvanSerem/prediccion-precipitacion-final

---

## 📌 1. Abstracto

En una primera etapa del recorrido formativo, se había trabajado sobre un problema agrícola más estructurado: la predicción del rendimiento de cultivos a partir de variables de suelo y clima. Ese enfoque permitió construir un modelo de alto desempeño para un entorno relativamente controlado.

En esta segunda etapa, el proyecto evolucionó hacia un problema más realista y desafiante: **comprender el comportamiento climático real de Argentina y modelar la precipitación a partir de datos históricos observados**.

El trabajo parte de datos obtenidos desde la API de **NASA POWER** para el período **2014–2023**, y se desarrolla en dos planos complementarios:

- por un lado, una **contextualización climática provincial**, orientada a describir patrones regionales, estacionalidad, frecuencia de lluvias y diferencias estructurales entre provincias;
- por otro, una **fase de Machine Learning**, centrada en el entrenamiento, validación, comparación, optimización y despliegue de un modelo de regresión para estimar precipitación.

Este proyecto puede resultar útil para:

- productores agrícolas,
- analistas del sector agroindustrial,
- profesionales vinculados a planificación climática,
- estudiantes de ciencia de datos aplicada al agro,
- perfiles interesados en el cruce entre datos reales, modelado y despliegue.

---

## 🎯 2. Objetivo del proyecto

El objetivo general del proyecto es **analizar el comportamiento climático real de Argentina y construir un sistema capaz de estimar la precipitación a partir de variables climáticas, espaciales y temporales**.

En términos prácticos, se buscó:

- validar y preparar un dataset climático real,
- identificar drivers relevantes del fenómeno,
- entrenar y comparar distintos modelos de regresión,
- evaluar overfitting y capacidad de generalización,
- optimizar hiperparámetros como parte del proceso metodológico,
- interpretar mejor la estructura interna de los datos,
- y transformar el modelo final en una herramienta interactiva de uso práctico.

---

## 📊 3. Resumen de metadata

**Fuente principal:** API oficial **NASA POWER**

### Características del conjunto de datos

- **83.996 registros diarios**
- **23 provincias argentinas**
- **Período:** 2014–2023

### Variables originales analizadas

- **Temperatura media diaria** (`temp_media`)
- **Temperatura máxima diaria** (`temp_max`)
- **Temperatura mínima diaria** (`temp_min`)
- **Precipitación diaria** (`precipitacion`)
- **Velocidad del viento** (`vel_viento`)
- **Humedad relativa** (`humedad`)
- **Fecha**
- **Provincia**
- **Latitud / Longitud**

### Tipo de datos

- numéricos continuos,
- variables temporales,
- variable categórica (`provincia`),
- variables derivadas creadas durante la ingeniería de atributos.

---

## ❓ 4. Preguntas / problema de investigación

### Primera parte: contextualización climática

- ¿Cuáles son las provincias con mayor temperatura media anual?
- ¿Qué provincias presentan mayor precipitación acumulada?
- ¿Cómo se distribuye la precipitación diaria?
- ¿La lluvia se concentra en eventos intensos o se distribuye de forma uniforme?
- ¿Qué provincias presentan mayor cantidad de rachas de lluvia?
- ¿Cuál es la frecuencia de días sin precipitaciones?
- ¿Cuáles son las provincias con mayor humedad relativa promedio?
- ¿Existen agrupamientos naturales de provincias según su comportamiento climático?

### Segunda parte: problema de Machine Learning

**¿Es posible estimar la precipitación a partir de variables climáticas, geográficas y temporales utilizando técnicas de Machine Learning?**

Este problema fue modelado como una tarea de **regresión supervisada**, donde la variable objetivo quedó definida como:

- **`precipitacion`**

---

## 🧪 5. Etapas desarrolladas

### 5.1 Validación inicial del dataset

Se realizó una revisión completa de la estructura del dataset para confirmar que estuviera en condiciones de avanzar hacia el modelado.

Se verificó:

- estructura general de variables,
- tipos de datos,
- valores nulos,
- dimensiones del conjunto,
- duplicados exactos y duplicados lógicos por provincia y fecha.

**Resultado:**  
El dataset no presentó valores nulos ni duplicados relevantes, lo que permitió avanzar sin necesidad de imputación ni eliminación de registros.

---

### 5.2 Diagnóstico de valores extremos

Se realizó un análisis de outliers combinando:

- diagnóstico estadístico mediante **IQR**,
- revisión visual con boxplots e histogramas,
- y validación de **plausibilidad física**.

Se confirmó que:

- no había humedades fuera de rango,
- no había precipitaciones negativas,
- no había velocidades de viento negativas,
- ni inconsistencias entre temperatura máxima, media y mínima.

**Conclusión:**  
Los valores extremos observados, especialmente en precipitación, fueron interpretados como parte de la variabilidad natural del fenómeno climático y no como errores de registro.

---

### 5.3 Transformación de variables categóricas

La variable `provincia` fue codificada mediante **One-Hot Encoding**, generando una representación numérica apta para los modelos de Machine Learning sin imponer jerarquías artificiales entre categorías.

---

### 5.4 Feature Selection

Se aplicaron dos enfoques para identificar variables relevantes:

- **SelectKBest con `f_regression`**
- **Importancia de variables con `RandomForestRegressor`**

Esto permitió detectar como drivers principales:

- humedad,
- temperaturas,
- latitud / longitud,
- y componentes temporales como `dia_del_anio`.

---

### 5.5 Ingeniería de atributos

Se crearon variables temporales y sintéticas para enriquecer la representación del problema.

#### Variables temporales

- `mes`
- `dia_del_anio`

#### Variables sintéticas

- `amplitud_termica`
- `humedad_x_temp`
- `viento_x_humedad`

Estas nuevas features ayudaron a capturar interacciones más complejas entre variables atmosféricas.

---

### 5.6 Modelado predictivo

Se dividió el dataset en:

- **80% entrenamiento**
- **20% prueba**

Se entrenaron y compararon tres modelos de regresión:

- **Ridge Regression**
- **Random Forest Regressor**
- **CatBoost Regressor**

#### Comparación general

- **Ridge** funcionó como baseline lineal.
- **CatBoost** mostró un rendimiento intermedio.
- **Random Forest** se consolidó como la mejor alternativa en términos de desempeño general.

---

### 5.7 Análisis de overfitting

Se evaluó el desempeño del mejor modelo comparando métricas entre train y test.

El análisis mostró una diferencia entre entrenamiento y prueba, evidenciando que el modelo **Random Forest** presentaba señales de **overfitting**, incluso después de incorporar variables sintéticas. Aun así, esa brecha se redujo levemente luego de la ingeniería de atributos, lo que sugiere una mejora parcial en la representación del problema sin resolver por completo el desafío de generalización.

---

### 5.8 Optimización de hiperparámetros

Se utilizó **RandomizedSearchCV** para explorar configuraciones alternativas del modelo Random Forest.

#### Mejores hiperparámetros encontrados

- `n_estimators = 200`
- `max_depth = 15`
- `min_samples_split = 5`
- `min_samples_leaf = 1`
- `max_features = "log2"`

El mejor score promedio obtenido durante la búsqueda fue **R² = 0.3175**, valor inferior al observado previamente para la versión base en validación cruzada. Por eso, esta etapa se conserva como parte del recorrido metodológico, pero no modificó la elección final del modelo.

---

### 5.9 Validación cruzada

Se aplicó **validación cruzada de 5 folds** sobre los modelos principales y luego sobre la variante optimizada de Random Forest.

La comparación permitió observar que:

- **Random Forest base** mostró mejor rendimiento promedio y menor variabilidad que el modelo optimizado.
- **Ridge Regression** mantuvo un desempeño claramente inferior.
- la validación cruzada funcionó como una herramienta de estabilidad interna sobre el conjunto de entrenamiento.

Esto reforzó la decisión de conservar la versión base del modelo como alternativa final más sólida.

---

### 5.10 Análisis multivariado e interpretación

Se aplicó **PCA (Principal Component Analysis)** para explorar la estructura interna del dataset.

El análisis mostró que:

- los **dos primeros componentes** explican aproximadamente el **65,7%** de la varianza,
- con **cuatro componentes** se alcanza cerca del **88,6%**,
- y con **seis componentes** se supera el **96%** de varianza explicada acumulada.

Además, el PCA permitió observar que las variables térmicas, la humedad, la ubicación geográfica y las variables sintéticas organizan buena parte de la estructura multivariada del sistema. También reveló redundancias internas esperables, como la presencia de combinaciones lineales exactas derivadas de variables construidas.

---

## 🤖 6. Modelo final seleccionado

### **Random Forest Regressor base**

Entre los modelos evaluados, el enfoque con mejor desempeño general fue **Random Forest Regressor**.

Como parte del proceso metodológico, este modelo también fue optimizado mediante **RandomizedSearchCV**. Sin embargo, al comparar la versión optimizada contra la versión base en el conjunto de prueba, se observó que la **versión base** obtuvo mejores resultados finales.

Por este motivo, el análisis del modelo optimizado se conserva como parte del recorrido experimental del proyecto, pero el **modelo final seleccionado** es el **Random Forest Regressor base**, por haber mostrado mejor capacidad de generalización sobre datos no vistos.

### Métricas más relevantes

#### En test (modelo final seleccionado)

- **R² = 0.4599**
- **MAE = 2.0299**
- **RMSE = 5.7036**

#### En validación cruzada

- **R² promedio = 0.3353**
- **Desvío estándar = 0.0135**
- **MAE promedio = 2.1809**
- **RMSE promedio = 6.8115**

#### Comparación con la versión optimizada en test

**Random Forest base**
- **R² = 0.4599**
- **MAE = 2.0299**
- **RMSE = 5.7036**

**Random Forest optimizado**
- **R² = 0.3901**
- **MAE = 2.2031**
- **RMSE = 6.0606**

### Interpretación

El modelo logra capturar una parte moderada de la variabilidad de la precipitación.

Esto **no** debe interpretarse como un “porcentaje de aciertos”, sino como una **capacidad explicativa moderada** dentro de un problema de regresión. En otras palabras, el modelo consigue aprender parte de la lógica histórica del fenómeno, aunque no su totalidad.

---

## 🌧️ 7. Prueba práctica del modelo

Se desarrolló una función predictiva que permite ingresar nuevas condiciones climáticas y obtener una estimación de precipitación.

### Variables de entrada

- temperatura media
- temperatura máxima
- temperatura mínima
- humedad
- velocidad del viento
- latitud
- longitud
- día del año
- provincia

A partir de esos inputs, el sistema genera automáticamente las variables sintéticas necesarias y devuelve una predicción de precipitación.

### Observación

La prueba práctica se ejecutó correctamente utilizando el **Random Forest base**, seleccionado como modelo final del proyecto. Para el escenario evaluado, el modelo devolvió una predicción de aproximadamente **0.108 mm**, lo que sugiere una precipitación muy baja o prácticamente nula bajo esas condiciones.

Además, se verificó la consistencia entre la predicción obtenida en **Colab** y la generada en el despliegue de **Hugging Face Spaces**, utilizando exactamente los mismos datos de entrada, el mismo modelo exportado y la misma lógica de construcción de variables.

---

## 🚀 8. Despliegue interactivo

En la etapa final, el modelo fue transformado en una herramienta accesible mediante una aplicación web construida con **Gradio** y desplegada en **Hugging Face Spaces**.

La app permite:

- ingresar variables climáticas,
- simular escenarios,
- obtener una estimación inmediata de precipitación,
- y explorar de manera práctica el comportamiento del modelo.

🔗 **Probar el modelo en vivo:**  
https://huggingface.co/spaces/IvanSerem/prediccion-precipitacion-final

---

## 🔎 9. Principales insights del proyecto

- La precipitación no depende de un solo factor, sino de una combinación entre **humedad, temperatura, ubicación y estacionalidad**.
- Las variables con mayor capacidad explicativa fueron:
  - **humedad**
  - **temperaturas** (`temp_min`, `temp_media`, `temp_max`)
  - **latitud / longitud**
  - **`dia_del_anio`**
  - variables sintéticas como `amplitud_termica`, `humedad_x_temp` y `viento_x_humedad`
- Las variables sintéticas aportaron valor, aunque no eliminaron por completo el problema de generalización.
- La exclusión de **`anio`** permitió una formulación más simple sin deteriorar de forma relevante el desempeño final.
- El análisis mostró señales de **overfitting**, por lo que la validación cruzada fue clave para complementar la evaluación tradicional.
- El PCA confirmó que una parte importante de la estructura del dataset puede resumirse en pocas dimensiones.
- El despliegue final permitió convertir el modelo en una herramienta práctica y no solo en un experimento de notebook.

---

## ⚙️ 10. Reproducibilidad

El proyecto puede ejecutarse en:

- **Google Colab**
- **Kaggle**
- **entorno local con Python 3.x**

### Dependencias principales

- `pandas`
- `numpy`
- `matplotlib`
- `seaborn`
- `scikit-learn`
- `catboost`
- `joblib`
- `gradio`

---

## ✅ 11. Conclusión

Este proyecto muestra que la precipitación puede estimarse parcialmente mediante **Machine Learning**, aunque dentro de un alcance analítico y no como un sistema de pronóstico meteorológico exacto.

El mejor modelo final fue **Random Forest Regressor base**. La optimización de hiperparámetros no mejoró el desempeño en test, las variables sintéticas aportaron valor a la representación del problema, y el despliegue final permitió convertir el modelo en una herramienta interactiva y funcional.

### Síntesis final

En términos generales, el proyecto demostró que la precipitación puede estimarse parcialmente a partir de variables climáticas, geográficas y temporales mediante técnicas de Machine Learning. Dentro de los modelos evaluados, **Random Forest Regressor base** fue el que ofreció el mejor equilibrio entre desempeño y capacidad de generalización, superando tanto al modelo lineal como a la versión optimizada por hiperparámetros.

La incorporación de variables sintéticas aportó valor al representar mejor ciertas interacciones del sistema climático, mientras que la exclusión de la variable `anio` permitió simplificar la formulación sin deteriorar de forma relevante el rendimiento del modelo. Aunque persiste cierto nivel de overfitting y el resultado no debe interpretarse como un sistema de pronóstico meteorológico exacto, el trabajo logró construir una herramienta analítica consistente, defendible y aplicable, capaz de transformar patrones históricos en una estimación concreta de precipitación para nuevos escenarios.

---

## 👤 12. Autor

**Iván Seremczuk**  
Comisión 77750  
**Data Science II – Coderhouse**

# 🌾 DS2 – Proyecto Agrícola
## Contextualización Climática y Modelado Predictivo de Precipitación en Argentina (2014–2023)

Proyecto desarrollado para la cursada de **Data Science II** en **Coderhouse**, enfocado en el análisis de datos climáticos reales de Argentina y en la construcción de un modelo de **Machine Learning** capaz de estimar la precipitación a partir de variables meteorológicas, geográficas y temporales.

🔗 **Demo interactiva en Hugging Face Spaces:**  
https://huggingface.co/spaces/IvanSerem/prediccion-precipitacion-final

---

## 📌 Resumen del proyecto

El proyecto parte de datos climáticos históricos obtenidos desde la API de **NASA POWER** para el período **2014–2023** y se desarrolla en dos planos complementarios:

- una **contextualización climática provincial**, orientada a describir patrones regionales, estacionalidad, frecuencia de lluvias y diferencias estructurales entre provincias;
- una **fase de Machine Learning**, centrada en el entrenamiento, validación, comparación, optimización y despliegue de un modelo de regresión para estimar precipitación.

El objetivo general fue **analizar el comportamiento climático real de Argentina y construir un sistema capaz de estimar la precipitación a partir de variables climáticas, espaciales y temporales**.

---

## 📊 Dataset

**Fuente principal:** API oficial **NASA POWER**

### Características del conjunto de datos

- **83.996 registros diarios**
- **23 provincias argentinas**
- **Período:** 2014–2023

### Variables originales analizadas

- temperatura media diaria (`temp_media`)
- temperatura máxima diaria (`temp_max`)
- temperatura mínima diaria (`temp_min`)
- precipitación diaria (`precipitacion`)
- velocidad del viento (`vel_viento`)
- humedad relativa (`humedad`)
- fecha
- provincia
- latitud / longitud

### Variables derivadas

Durante la ingeniería de atributos se construyeron nuevas variables para enriquecer la representación del problema:

- temporales: `mes`, `dia_del_anio`
- sintéticas: `amplitud_termica`, `humedad_x_temp`, `viento_x_humedad`

---

## ❓ Problema de Machine Learning

**¿Es posible estimar la precipitación a partir de variables climáticas, geográficas y temporales utilizando técnicas de Machine Learning?**

El problema fue modelado como una tarea de **regresión supervisada**, donde la variable objetivo quedó definida como:

- **`precipitacion`**

---

## 🧪 Pipeline desarrollado

### 1. Validación y preparación del dataset
- revisión de estructura general
- verificación de valores nulos
- detección de duplicados exactos y lógicos
- diagnóstico de outliers
- validación de plausibilidad física

### 2. Transformación y enriquecimiento de datos
- **One-Hot Encoding** de `provincia`
- creación de variables temporales
- creación de variables sintéticas
- selección de variables relevantes mediante:
  - `SelectKBest`
  - importancia de variables con `RandomForestRegressor`

### 3. Modelado predictivo
Se entrenaron y compararon tres modelos:

- **Ridge Regression**
- **Random Forest Regressor**
- **CatBoost Regressor**

También se realizaron:
- análisis de overfitting
- validación cruzada de 5 folds
- optimización de hiperparámetros con `RandomizedSearchCV`
- comparación entre modelo base y modelo optimizado

### 4. Interpretación multivariada
Se aplicó **PCA (Principal Component Analysis)** para explorar la estructura interna del dataset y analizar la varianza explicada por los componentes principales.

### 5. Prueba práctica y despliegue
El modelo final se exportó y se integró en una aplicación construida con **Gradio** y desplegada en **Hugging Face Spaces**.

---

## 🤖 Modelo final seleccionado

### **Random Forest Regressor base**

Entre los modelos evaluados, el mejor desempeño general lo obtuvo **Random Forest Regressor**.

El modelo también fue sometido a una etapa de optimización con **RandomizedSearchCV**, pero al comparar resultados sobre el conjunto de prueba, la versión optimizada no superó a la versión base. Por eso, el **modelo final seleccionado** fue el **Random Forest Regressor base**, por haber mostrado mejor capacidad de generalización sobre datos no vistos.

---

## 📈 Métricas principales

### Desempeño en test del modelo final
- **R² = 0.4599**
- **MAE = 2.0299**
- **RMSE = 5.7036**

### Validación cruzada del modelo base (cv = 5)
- **R² promedio = 0.3353**
- **Desvío estándar = 0.0135**
- **MAE promedio = 2.1809**
- **RMSE promedio = 6.8115**

### Comparación con la versión optimizada en test

**Random Forest base**
- **R² = 0.4599**
- **MAE = 2.0299**
- **RMSE = 5.7036**

**Random Forest optimizado**
- **R² = 0.3901**
- **MAE = 2.2031**
- **RMSE = 6.0606**

---

## 🔎 Principales hallazgos

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

---

## 🌧️ Prueba práctica del modelo

Se desarrolló una función predictiva que permite ingresar nuevas condiciones climáticas y obtener una estimación de precipitación.

### Variables de entrada de la app
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

### Resultado de validación práctica
La prueba práctica se ejecutó correctamente utilizando el **Random Forest base**. Para el escenario evaluado, el modelo devolvió una predicción de aproximadamente **0.108 mm**, y se verificó consistencia entre la predicción obtenida en **Colab** y la generada en **Hugging Face Spaces**.

---

## 🚀 Despliegue interactivo

La etapa final transformó el modelo en una herramienta accesible mediante una aplicación web construida con **Gradio** y desplegada en **Hugging Face Spaces**.

La app permite:

- ingresar variables climáticas,
- simular escenarios,
- obtener una estimación inmediata de precipitación,
- explorar de forma práctica el comportamiento del modelo.

🔗 **Probar el modelo en vivo:**  
https://huggingface.co/spaces/IvanSerem/prediccion-precipitacion-final

---

## ⚙️ Reproducibilidad

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

## ✅ Conclusión

Este proyecto muestra que la precipitación puede estimarse parcialmente mediante **Machine Learning**, aunque dentro de un alcance analítico y no como un sistema de pronóstico meteorológico exacto.

El mejor modelo final fue **Random Forest Regressor base**. La optimización de hiperparámetros no mejoró el desempeño en test, las variables sintéticas aportaron valor a la representación del problema, y el despliegue final permitió convertir el modelo en una herramienta interactiva y funcional.

---

## 👤 Autor

**Iván Seremczuk**  
**Data Science II – Coderhouse**

# Alan-Palafox

# 💳 Credit Risk Scorecard: End-to-End Pipeline

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Data Science](https://img.shields.io/badge/Domain-Credit_Risk-success.svg)
![Machine Learning](https://img.shields.io/badge/Model-Logistic_Regression-orange.svg)

## 📌 Descripción del Proyecto
Este repositorio contiene un pipeline completo para la construcción de un modelo de riesgo crediticio (Credit Scoring). A diferencia de los modelos de "caja negra", este proyecto implementa una metodología estándar de la industria bancaria basada en **Weight of Evidence (WoE)** y **Regresión Logística**, culminando en la generación de una **Tarjeta de Puntuación (Scorecard)** explicable y lista para reglas de negocio.

## 🏗️ Arquitectura y Buenas Prácticas
Para garantizar la escalabilidad y el pase a producción, el código no está aglomerado en un solo script. Se utilizó un Jupyter Notebook como **orquestador**, delegando la lógica compleja a módulos independientes en Python:

| Archivo / Módulo | Descripción de su Función |
| :--- | :--- |
| 📓 `Main_Pipeline.ipynb` | Orquestador principal. Carga datos, llama a los módulos y visualiza resultados. |
| 🐍 `EDA_module.py` | Análisis Exploratorio de Datos, análisis de distribuciones y correlaciones. |
| 🐍 `preprocessing_vars.py` | Limpieza de datos, imputación de nulos y tratamiento de variables temporales. |
| 🐍 `credit_data_processing.py` | Optimización de memoria, cálculo de WoE, Information Value (IV) y escalado del Scorecard. |

## ⚙️ Metodología y Desarrollo

### 1. Preprocesamiento y Optimización
* **Optimización de Memoria:** Reducción del peso del dataset en RAM mediante *downcasting* dinámico de tipos numéricos.
* **Feature Engineering:** Tratamiento de fechas (ej. `issue_d`), manejo de outliers y creación de la variable objetivo (Buen/Mal pagador).

### 2. Selección Rigurosa de Variables (Feature Selection)
Se implementó un embudo estadístico para garantizar la robustez del modelo y evitar sobreajuste:
1. **Information Value (IV):** Filtrado de variables con bajo poder predictivo.
2. **Análisis de Correlación:** Eliminación de variables altamente correlacionadas.
3. **Variance Inflation Factor (VIF):** Detección y mitigación de multicolinealidad.
4. **P-Values:** Retención exclusiva de variables estadísticamente significativas (p-value < 0.05) usando `statsmodels`.

### 3. Modelado y Generación del Scorecard
Se entrenó una Regresión Logística utilizando las variables transformadas a WoE. Posteriormente, los coeficientes del modelo se tradujeron a puntos de negocio utilizando los siguientes parámetros estándar de la industria:

| Parámetro del Scorecard | Valor Configurado |
| :--- | :--- |
| **Base Score (Target Score)** | 600 puntos |
| **Points to Double the Odds (PDO)** | 25 puntos |
| **Target Odds** | (Configurable según el apetito de riesgo) |

## 📊 Resultados y Evaluación
El modelo se evaluó utilizando métricas exigidas por la regulación de Basilea y las mejores prácticas de riesgo:
* **Curva ROC y AUC:** Para medir la capacidad general de discriminación del modelo.
* **Estadístico Kolmogorov-Smirnov (KS):** Calculado programáticamente para encontrar el punto máximo de separación (cutoff) entre la distribución de buenos y malos clientes.
* **Índice Gini:** Como medida de desigualdad y concentración de riesgo.

## 🚀 Cómo ejecutar este proyecto

1. > 💻 **¿Quieres ver el código, descargar el dataset y clonar este proyecto?** 
> 👉 [**Haz clic aquí para ir al repositorio oficial en GitHub**](https://github.com/Alan-Palafox-Geophysics/Credit_Scoring)

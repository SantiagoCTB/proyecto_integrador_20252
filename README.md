# Pronóstico de afluencia del Metro de Medellín

Este repositorio contiene el material del proyecto integrador para anticipar la cantidad de pasajeros en el sistema Metro de Medellín (trenes, tranvía y cables) a partir de datos históricos 2019-2025. El trabajo combina análisis exploratorio, ingeniería de variables de series temporales y modelos de aprendizaje automático para estimar la demanda por línea y hora con el fin de apoyar la planeación operativa.

## Estructura del repositorio
- `afluencia.ipynb`: cuaderno principal con la preparación de datos, análisis exploratorio, creación de variables exógenas (festivos, calendarios, ventanas móviles) y entrenamiento de modelos de pronóstico.
- `datasets/Afluencia_Metro_2019-2025.xlsx`: fuente de datos consolidada con el histórico de afluencia por fecha, hora y línea.
- `Modelos ML/`: artefactos de modelos entrenados (`best_xgboost_regressor.joblib`, `random_forest_regressor.joblib`, `xgboost_regressor.joblib`).
- `Entrega final/`: documentación académica del proyecto.

## Requisitos
Se sugiere un entorno con Python 3.10+ y las siguientes dependencias utilizadas en el cuaderno:

```
pandas
numpy
matplotlib
seaborn
scikit-learn
xgboost
sktime
holidays
joblib
```

Puedes instalarlas con `pip install -r requirements.txt` si preparas un archivo, o manualmente con `pip install <paquete>`.

## Uso
1. Clona el repositorio y coloca el archivo de datos en `datasets/` (ya está incluido para referencia local).
2. Abre `afluencia.ipynb` en Jupyter o VS Code y ejecuta las celdas de preparación: limpieza, agregaciones por fecha/hora/línea y creación de variables de calendario.
3. Ejecuta las secciones de modelado para reproducir el ajuste de modelos SARIMA y los enfoques de Machine Learning (Random Forest y XGBoost) sobre las características tabulares generadas.
4. Los modelos entrenados se guardan automáticamente en `Modelos ML/`; puedes cargarlos en nuevas sesiones con `joblib.load` para inferencia.

## Detalles metodológicos
- **Enfoque temporal**: división cronológica tipo _train/validation/test_ con énfasis en datos posteriores a 2022 para evitar distorsiones de la pandemia. El cuaderno utiliza `sktime` para asegurar cortes respetando el orden temporal.
- **Variables**: fecha y hora, identificador de línea, indicadores de fin de semana/festivo (usando `holidays`), retardos (lags) y ventanas móviles de afluencia para capturar tendencia y estacionalidad.
- **Modelos probados**: SARIMA para referencia, además de regresores de bosque aleatorio y XGBoost sobre la representación tabular. Se incluye el mejor modelo ajustado (`best_xgboost_regressor.joblib`) tras búsqueda de hiperparámetros.

## Resultados esperados
El flujo reproduce métricas de error (MSE/RMSE) en validación y prueba para comparar modelos y seleccionar el mejor desempeño. Los gráficos de dispersión, residuales y pronósticos por línea ayudan a interpretar el ajuste y a identificar horarios de mayor congestión.

## Equipo
Proyecto desarrollado por el Equipo #5 de la Maestría en Ciencia de Datos y Analítica.

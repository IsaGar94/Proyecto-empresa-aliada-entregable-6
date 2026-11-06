## 1. Propósito del proyecto

En este entregable se desarrolla un ejercicio de predicción de ventas para las marcas VANISH y LYSOL, utilizando la variable `TOTAL_UNIT_SALES`. Se implementan dos enfoques de modelado: regresión lineal y modelos ARIMA. Los datos históricos de cada marca se dividen en conjuntos de entrenamiento y prueba para ajustar los modelos, generar predicciones y evaluar su desempeño.

## 2. Objetivo

Construir y evaluar modelos que permitan estimar las ventas de VANISH y LYSOL a partir de su comportamiento histórico. Para ello, se realiza una división 90/10, se ajustan modelos de regresión lineal, se evalúan sus predicciones y se comparan distintos órdenes ARIMA mediante el criterio AIC.

## 3. Datos utilizados

El análisis se realiza por separado para las marcas **VANISH** y **LYSOL**. La variable objetivo es `TOTAL_UNIT_SALES`, que representa las unidades vendidas. La columna `DATE` permite identificar el periodo de cada observación y presentar los resultados gráficamente. Se parte de los conjuntos previamente preparados `df_vanish` y `df_lysol`.

## 4. Herramientas y tecnologías utilizadas

- **Python:** lenguaje utilizado para el análisis.
- **NumPy:** generación de índices numéricos y operaciones auxiliares.
- **Pandas:** manipulación de series y organización de resultados.
- **Scikit-learn:** implementación de regresión lineal y métricas de evaluación.
- **Statsmodels:** ajuste y evaluación de modelos ARIMA.
- **Matplotlib:** elaboración de gráficas.

## 5. Desarrollo del proyecto

### 5.1. División de los datos

Para cada marca se utiliza el 90 % de las observaciones como conjunto de entrenamiento y el 10 % restante como conjunto de prueba. La separación conserva el orden de los registros: las primeras observaciones se destinan al entrenamiento y las últimas al conjunto de prueba.

### 5.2. Preparación de la variable independiente

Para la regresión lineal se genera un índice numérico consecutivo que representa la posición temporal de cada observación. Se construyen las variables independientes de entrenamiento y prueba para VANISH y LYSOL, manteniendo la continuidad de los índices entre ambos conjuntos.

### 5.3. Modelo de regresión lineal

Se utiliza `LinearRegression` de Scikit-learn para crear un modelo independiente por marca. Cada modelo se ajusta con el índice temporal como variable independiente y `TOTAL_UNIT_SALES` como variable objetivo. Posteriormente, se obtienen el intercepto y la pendiente de cada modelo.

### 5.4. Predicciones de regresión lineal

Una vez entrenados los modelos, se generan predicciones para las observaciones del conjunto de prueba. Los resultados se organizan en tablas que muestran la fecha, las ventas reales y las ventas predichas para cada marca.

### 5.5. Evaluación de la regresión lineal

El desempeño se evalúa mediante las siguientes métricas:

- **MAE (Mean Absolute Error):** promedio de los errores absolutos entre los valores reales y las predicciones.
- **RMSE (Root Mean Squared Error):** raíz del promedio de los errores cuadrados; da mayor peso a los errores de mayor magnitud.
- **Error relativo:** MAE dividido entre el promedio de las ventas reales del conjunto de prueba y multiplicado por 100.

La función `interpretar_error` clasifica el error relativo de acuerdo con los siguientes rangos:

| Error relativo | Interpretación |
|---|---|
| Menor a 5 % | Muy bueno |
| De 5 % a menos de 10 % | Bueno |
| De 10 % a menos de 20 % | Moderado |
| De 20 % a 30 % | Alto |
| Mayor a 30 % | Muy alto |

### 5.6. Gráficas de regresión lineal

Se generan gráficas independientes para VANISH y LYSOL. En ellas se muestran las ventas históricas y las predicciones correspondientes al conjunto de prueba, lo que permite observar la tendencia estimada y contrastarla con las ventas registradas.

### 5.7. Construcción de modelos ARIMA

Como segundo enfoque, se ajustan modelos ARIMA para cada marca utilizando sus datos de entrenamiento. Se prueban los siguientes órdenes:

- ARIMA (0,1,0)
- ARIMA (1,1,0)
- ARIMA (0,1,1)
- ARIMA (1,1,1)
- ARIMA (2,1,0)
- ARIMA (0,1,2)

### 5.8. Selección del mejor modelo mediante AIC

Para cada modelo ARIMA se obtiene el criterio de información de Akaike (AIC). Los valores se comparan y se selecciona, para cada marca, el modelo con el AIC más bajo entre los órdenes evaluados.

### 5.9. Pronósticos ARIMA para el conjunto de prueba

Con el mejor modelo seleccionado para cada marca se generan pronósticos cuyo número de pasos corresponde al tamaño del conjunto de prueba. También se calculan intervalos de confianza del 90 %, mediante `alpha=0.10`, para obtener un límite inferior y uno superior para cada pronóstico.

### 5.10. Visualización de resultados ARIMA

Se construye una gráfica independiente para cada marca. Las visualizaciones incluyen los datos de entrenamiento, los datos reales de prueba, las predicciones del modelo ARIMA seleccionado y los límites inferior y superior del intervalo de confianza del 90 %. El título indica el orden ARIMA seleccionado.

## 6. Resultado del proyecto

Se obtienen modelos de regresión lineal y modelos ARIMA para VANISH y LYSOL. Para la regresión lineal se calculan predicciones y métricas de evaluación; para ARIMA se comparan seis órdenes mediante AIC y se generan pronósticos para el conjunto de prueba con intervalos de confianza del 90 %. El entregable incluye tablas y gráficas para analizar el desempeño de los modelos frente a las ventas reales.

- La división 90/10 conserva el orden de las observaciones; el conjunto de prueba corresponde a los registros finales.
- Los modelos se ajustan por separado para VANISH y LYSOL.
- El índice de la regresión lineal representa la posición de cada observación; no incorpora por sí mismo variables adicionales como estacionalidad o efectos de calendario.
- El AIC se utiliza para comparar los modelos ARIMA evaluados para una misma serie.
- Los intervalos de confianza del 90 % expresan incertidumbre alrededor de los pronósticos; no garantizan que los valores reales se encuentren dentro de ellos.
- El código presentado genera pronósticos para el conjunto de prueba. No incluye un pronóstico adicional de seis periodos futuros.
- La calidad de las predicciones debe interpretarse considerando la cantidad de observaciones disponibles y el comportamiento histórico de cada marca.

## 7. Conclusión

En este entregable se implementan dos enfoques para analizar y predecir las ventas de VANISH y LYSOL. La regresión lineal estima una tendencia a partir del índice temporal, mientras que ARIMA ofrece una alternativa basada en la estructura temporal de cada serie.

La evaluación mediante MAE, RMSE y error relativo, junto con la comparación de órdenes ARIMA mediante AIC, proporciona elementos para contrastar el desempeño de los modelos. Las gráficas complementan el análisis al mostrar las predicciones frente a los datos reales y sus intervalos de confianza.

## 8. Estructura general del proyecto

```text
Proyecto/
│
├── Datos preparados por marca
│   ├── df_vanish
│   └── df_lysol
│
└── Análisis de predicción de ventas
    ├── División entrenamiento y prueba
    ├── Regresión lineal
    ├── Evaluación de modelos
    ├── Selección de modelos ARIMA mediante AIC
    ├── Pronósticos e intervalos de confianza
    └── Gráficas de resultados
```
**Nota:** El archivo `Productos.csv` corresponde a la base de datos consolidada en el entregable anterior. Las visualizaciones se generan y guardan al ejecutar el código en el directorio de trabajo.

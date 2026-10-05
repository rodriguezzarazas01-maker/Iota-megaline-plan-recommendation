# Ι Proyecto Iota | Recomendación de Planes de Megaline

## Descripción

Megaline busca migrar a sus clientes desde planes heredados hacia sus nuevas tarifas comerciales: **Smart** y **Ultra**. Para facilitar este proceso, la compañía necesita un modelo capaz de analizar el comportamiento mensual de los usuarios y recomendar automáticamente el plan más adecuado.

En este proyecto se desarrollaron modelos de clasificación supervisada utilizando información histórica de clientes que ya utilizan los nuevos planes. El objetivo fue construir un modelo con la mayor exactitud posible para predecir qué tarifa se adapta mejor a cada usuario en función de sus patrones de consumo.

## Objetivos

- Explorar y comprender el conjunto de datos.
- Preparar los datos para el entrenamiento de modelos de clasificación.
- Dividir la información en conjuntos de entrenamiento, validación y prueba.
- Entrenar diferentes algoritmos de Machine Learning.
- Ajustar hiperparámetros para optimizar el rendimiento.
- Comparar el desempeño de distintos modelos.
- Seleccionar el modelo con mayor exactitud.
- Verificar que el modelo supere el umbral mínimo de exactitud establecido por Megaline.
- Realizar una prueba de cordura para validar los resultados obtenidos.

## Herramientas utilizadas

- Python
- Pandas
- NumPy
- Scikit-Learn
- Matplotlib
- Jupyter Notebook

## Fuente de datos

Archivo utilizado:

- `users_behavior.csv`

Variables disponibles:

- `calls` — número de llamadas realizadas.
- `minutes` — duración total de llamadas en minutos.
- `messages` — cantidad de mensajes enviados.
- `mb_used` — tráfico de internet utilizado en MB.
- `is_ultra` — variable objetivo:
  - 1 = Ultra
  - 0 = Smart

## Metodología

### 1. Exploración inicial de los datos

Se realizó una revisión general del conjunto de datos para verificar:

- Estructura del dataset.
- Tipos de datos.
- Valores ausentes.
- Registros duplicados.

La revisión confirmó que la información estaba lista para ser utilizada en modelos de clasificación sin requerir procesos complejos de limpieza.

### 2. Preparación del problema de clasificación

Se creó una variable categórica denominada:

```text
Name_plan
```

para representar explícitamente las dos clases del problema:

- Smart
- Ultra

Posteriormente se definieron:

- Variables predictoras (features).
- Variable objetivo (target).

### 3. División de los datos

El conjunto de datos fue dividido mediante estratificación para conservar la distribución original de clases:

- Entrenamiento: 60%
- Validación: 20%
- Prueba: 20%

La proporción de usuarios de los planes Smart y Ultra permaneció prácticamente idéntica en todos los subconjuntos, garantizando una evaluación consistente de los modelos.

### 4. Entrenamiento de modelos

#### Árbol de decisión

Se evaluaron distintos niveles de profundidad para identificar la configuración que maximizara la exactitud.

Mejor resultado:

```text
max_depth = 8
```

Exactitud obtenida:

```text
79.63%
```

#### Bosque aleatorio

Se analizaron distintas combinaciones de:

- Número de árboles.
- Profundidad máxima.

Mejor resultado:

```text
n_estimators = 76
max_depth = 12
```

Exactitud obtenida:

```text
81.34%
```

### 5. Comparación de modelos

| Modelo | Accuracy |
|----------|----------:|
| Decision Tree | 79.63% |
| Random Forest | 81.34% |

El modelo Random Forest obtuvo el mejor desempeño y fue seleccionado para la evaluación final.

### 6. Evaluación sobre el conjunto de prueba

Una vez seleccionado el modelo óptimo, se realizó la evaluación utilizando datos que no participaron ni en el entrenamiento ni en la validación.

Resultado final:

```text
Accuracy = 81.80%
```

Este valor supera ampliamente el umbral mínimo exigido por Megaline:

```text
Accuracy > 75%
```

### 7. Prueba de cordura

Para verificar que el modelo realmente aprendió patrones útiles y no simplemente aprovechó la distribución de clases, se construyó un modelo base utilizando:

```text
DummyClassifier(strategy="most_frequent")
```

Resultados:

| Modelo | Accuracy |
|----------|----------:|
| Dummy Classifier | 69.36% |
| Random Forest | 81.34% |

La diferencia observada confirma que el modelo seleccionado aporta una mejora significativa respecto a una estrategia trivial.

## Principales hallazgos

- El conjunto de datos presentó una buena calidad inicial.
- Las clases permanecieron correctamente balanceadas después de la división estratificada.
- El árbol de decisión logró superar el umbral mínimo requerido por el proyecto.
- Random Forest obtuvo el mejor desempeño entre los modelos evaluados.
- La exactitud final superó el 81%.
- La prueba de cordura confirmó que el modelo captura patrones reales del comportamiento de los usuarios.

## Modelos evaluados

### Decision Tree Classifier

Ventajas observadas:

- Fácil interpretación.
- Entrenamiento rápido.
- Buen desempeño inicial.

Limitaciones:

- Menor capacidad de generalización frente a Random Forest.

### Random Forest Classifier

Ventajas observadas:

- Mayor exactitud.
- Mejor capacidad de generalización.
- Mayor estabilidad frente a variaciones de los datos.

Resultado:

- Modelo seleccionado para producción.

## Visualizaciones desarrolladas

- Distribución de clases en el dataset original.
- Comparación de la distribución de clases entre entrenamiento, validación y prueba.
- Evolución de la exactitud del árbol de decisión según la profundidad.
- Comparación de exactitud entre distintos modelos.

## Archivos principales

- `iota_megaline_plan_recommendation.ipynb`
- `users_behavior.csv`

## Conclusión

El proyecto permitió desarrollar un modelo de Machine Learning capaz de recomendar automáticamente uno de los nuevos planes comerciales de Megaline a partir del comportamiento mensual de los usuarios.

Tras comparar diferentes algoritmos de clasificación, el modelo **Random Forest** obtuvo el mejor desempeño, alcanzando una exactitud cercana al **82%** sobre datos no vistos previamente. Este resultado supera con holgura el umbral mínimo requerido por la compañía y demuestra que los patrones de llamadas, mensajes y consumo de internet contienen suficiente información para distinguir entre usuarios de los planes Smart y Ultra.

Además, la prueba de cordura confirmó que el modelo seleccionado ofrece un rendimiento considerablemente superior al de una estrategia basada únicamente en seleccionar la clase más frecuente.

Desde una perspectiva de negocio, los resultados indican que Megaline puede utilizar técnicas de aprendizaje automático para automatizar la recomendación de planes, facilitar la migración de clientes a las nuevas tarifas y mejorar la personalización de sus estrategias comerciales.

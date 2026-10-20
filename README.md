#### Predicción del Riesgo de Diabetes mediante el Proceso KDD

## Descripción del proyecto

Este proyecto aplica el proceso **KDD (Knowledge Discovery in Databases)** para analizar datos de pacientes e identificar patrones asociados al riesgo de desarrollar diabetes. Mediante técnicas de minería de datos y un árbol de decisión, se construye un modelo de clasificación capaz de categorizar el riesgo de los pacientes en tres niveles: **Low (bajo), Moderate (moderado) y High (alto)**.

El proyecto destaca la importancia de las etapas de selección, limpieza, transformación, minería de datos e interpretación de resultados para convertir datos en conocimiento útil.

## Objetivos

- Aplicar la metodología KDD a un conjunto de datos relacionado con la diabetes.
- Identificar las variables más relevantes para clasificar el riesgo de diabetes.
- Construir un modelo predictivo interpretable mediante árboles de decisión.
- Evaluar el desempeño del modelo utilizando datos de prueba.
- Interpretar los patrones encontrados como apoyo a la identificación de pacientes que podrían requerir seguimiento clínico.

## Dataset

Se utilizó el conjunto de datos `diabetes_risk.csv`, compuesto por **15,000 registros y 19 variables**.

Las variables se agrupan en las siguientes categorías:

- **Demográficas:** edad, género, ciudad y nivel de ingresos.
- **Clínicas y biométricas:** glucosa en ayunas, hemoglobina glucosilada (HbA1c), índice de masa corporal, presión arterial y circunferencia de cintura.
- **Hábitos y estilo de vida:** actividad física, alimentación, tabaquismo, consumo de alcohol, horas de sueño y nivel de estrés.
- **Antecedentes familiares:** historial de diabetes.
- **Variable objetivo:** `diabetes_risk`, con las categorías `Low`, `Moderate` y `High`.

La columna `patient_id` se descartó por tratarse de un identificador único sin utilidad predictiva directa.

## Metodología KDD

### 1. Selección de los datos
Se identificaron las variables relevantes para el análisis y se definió `diabetes_risk` como variable objetivo.

### 2. Limpieza de datos
Se verificó la existencia de registros duplicados y valores faltantes.

- No se encontraron registros duplicados.
- Los valores ausentes de `smoking_status`, `alcohol_consumption` e `income_bracket` se reemplazaron por la categoría `Unknown`.
- Se eliminó la variable identificadora `patient_id`.

### 3. Transformación de los datos
Las variables categóricas y la variable objetivo se transformaron al tipo `factor`, requerido para el modelado utilizado en R.

La distribución de la variable objetivo fue:

| Categoría | Proporción |
|---|---:|
| Low | 60 % |
| Moderate | 25 % |
| High | 15 % |

Posteriormente, los datos se dividieron en **70 % para entrenamiento y 30 % para prueba**, mediante muestreo estratificado para conservar la proporción de las categorías.

### 4. Minería de datos
Se implementó un árbol de decisión mediante el algoritmo CART, utilizando la función `rpart` de R.

Parámetros principales:

- `cp = 0.001`
- `minsplit = 20`
- `maxdepth = 4`

El árbol inicial se podó mediante la selección del parámetro de complejidad asociado al menor error de validación cruzada, con el propósito de obtener un modelo más sencillo e interpretable.

### 5. Evaluación e interpretación
El modelo se evaluó con los datos de prueba mediante una matriz de confusión y métricas de clasificación, incluyendo exactitud global (*accuracy*), sensibilidad, especificidad e importancia relativa de las variables.

## Principales resultados

El árbol de decisión identificó las siguientes variables como relevantes para la clasificación del riesgo:

1. **Glucosa en ayunas (`fasting_blood_sugar`):** principal variable de división del árbol. Los valores elevados, especialmente a partir de 212 según los umbrales identificados, se asociaron con una mayor concentración de casos clasificados como riesgo alto.
2. **Hemoglobina glucosilada (`hba1c_level`):** segundo criterio relevante para distinguir entre los niveles de riesgo.
3. **Edad (`age`):** contribuye a refinar la clasificación de los pacientes.
4. **Circunferencia de cintura (`waist_circumference_cm`):** ayuda a diferenciar grupos de riesgo bajo y moderado.

Los resultados muestran cómo un modelo interpretable puede revelar relaciones entre variables clínicas y categorías de riesgo.

## Tecnologías y herramientas

- **R:** procesamiento de datos y construcción del modelo.
- **rpart:** implementación del árbol de decisión CART.
- **caret:** partición estratificada de los datos mediante `createDataPartition`.
- **KDD:** metodología para el descubrimiento de conocimiento a partir de datos.
- **Minería de datos y aprendizaje automático:** clasificación supervisada y evaluación del modelo.

## Conclusiones

El proyecto demuestra la aplicación práctica del proceso KDD para transformar un conjunto de datos en conocimiento interpretable. El árbol de decisión permitió identificar la glucosa en ayunas y la hemoglobina glucosilada como las variables más relevantes, seguidas de la edad y la circunferencia de cintura.

Además, el trabajo evidencia que la calidad de los datos, su transformación y la validación del modelo son etapas fundamentales para obtener resultados útiles. Como posible trabajo futuro, se propone comparar el árbol de decisión con algoritmos como Random Forest y regresión logística para estudiar posibles mejoras en el desempeño predictivo.

**Nota:** Este modelo tiene fines académicos y de análisis de datos. Sus resultados no constituyen un diagnóstico médico ni sustituyen la evaluación de un profesional de la salud.

## Autores

- Jorge Luis Ortiz Libreros
- Joshua Iván Olivares Blanco
- Fabiola López Velázquez


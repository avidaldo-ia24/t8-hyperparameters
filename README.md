# Tarea 8: Optimización de hiperparámetros

1. Crea un nuevo repositorio de trabajo en [avidaldo-ia24](https://github.com/organizations/avidaldo-ia24/repositories/new):
    - `Owner` debe ser `avidaldo-ia24`.
    - El nombre debe ser `t8-hyperparameters-nombre1-apellido1`, sustituyendo `nombre1-apellido1` por tu identificador.
    - Ese nuevo repositorio debe ser **privado**.

2. Partiremos del [proyecto de predicción del precio medio de viviendas por distrito de California](https://github.com/avidaldo/ia24#precio-medio-de-viviendas-por-distrito-de-california-regresi%C3%B3n).

> [!TIP]
> Revisa los notebooks de este proyecto. Aparte de otras pequeñas mejoras, se han añadido dos nuevos notebook:
> - [Transformadores personalizados](https://github.com/avidaldo/ia24/blob/main/end2end/e2e051_custom_transformers.ipynb)
> - [Uso de KMeans en el transformador personalizado para tratar los datos de geolocalización](https://github.com/avidaldo/ia24/blob/main/end2end/e2e060_spatial_clustering.ipynb).

3. Crea un nuevo notebook en tu repositorio llamado "tarea8.ipynb" sobre optimización de hiperparámetros.
    - Define el pipeline con el preprocesamiento y un modelo Random Forest.
    - Carga los datos y prepáralos para el entrenamiento.
    - Investiga los hiperparámetros configurables de Random Forest.
    - Investiga cómo usar GridSearchCV o RandomizedSearchCV para buscar mejores hiperparámetros para el modelo.
        - Prueba distintos números de clusters para el KMeans.
        - Prueba distintos n_estimators, max_features, max_depth, min_samples_leaf y min_samples_split para el Random Forest.
    - Selecciona los mejores hiperparámetros y evalúa el modelo con ellos usando el conjunto de test.

4. Entrega en el aula virtual el commit de tu repositorio con el notebook terminado.


Ejemplo de uso de GridSearchCV:

```python
from sklearn.model_selection import GridSearchCV
from sklearn.ensemble import RandomForestClassifier

full_pipeline = Pipeline([
    ("preprocessing", preprocessing),
    ("random_forest", RandomForestRegressor(random_state=42)),
])
param_grid = [
    {'preprocessing__geo__n_clusters': [5, 8, 10],
     'random_forest__max_features': [4, 6, 8]},
    {'preprocessing__geo__n_clusters': [10, 15],
     'random_forest__max_features': [6, 8, 10]},
]
grid_search = GridSearchCV(full_pipeline, param_grid, cv=3,
                           scoring='neg_root_mean_squared_error')
grid_search.fit(housing, housing_labels)

```

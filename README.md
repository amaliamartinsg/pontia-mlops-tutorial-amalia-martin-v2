# Adult Income Classification Project

Este proyecto implementa un pipeline de Machine Learning para predecir si una persona gana más de 50K al año usando el dataset "Adult" del UCI Machine Learning Repository. El flujo completo incluye descarga de datos, preprocesamiento, entrenamiento, evaluación y registro del modelo en MLflow.

## Estructura del Proyecto

- **src/**: Código fuente principal
  - `main.py`: Orquestador del pipeline de entrenamiento y evaluación
  - `data_loader.py`: Carga y preprocesa los datos
  - `model.py`: Entrenamiento del modelo (RandomForestClassifier)
  - `evaluate.py`: Evaluación del modelo
- **data/raw/**: Carpeta donde se descargan los datos originales
- **models/**: Carpeta donde se guardan los modelos entrenados y artefactos
- **scripts/register_model.py**: Script para registrar el modelo entrenado en MLflow
- **unit_tests/**: Pruebas unitarias para los módulos principales

## Pipeline de Entrenamiento

1. **Descarga de datos**: Se descargan los archivos `adult.data` y `adult.test`.
2. **Carga y preprocesamiento**: Se leen los datos, se limpian, codifican las variables categóricas y se escalan las numéricas.
3. **Entrenamiento**: Se entrena un modelo RandomForestClassifier usando scikit-learn.
4. **Evaluación**: Se evalúa el modelo en el conjunto de test y se reportan métricas como accuracy y classification report.
5. **Registro**: El modelo, el scaler y los encoders se guardan y el modelo se registra en MLflow para su gestión y versionado.

## Ejecución

1. Instala las dependencias:
   ```bash
   pip install -r requirements.txt
   ```
2. Añade los datos en `data/raw/` de `https://archive.ics.uci.edu/ml/machine-learning-databases/adult/adult.data`.
3. Ejecuta el pipeline de entrenamiento:
   ```bash python src/main.py```
4. (Opcional) Ejecuta los tests:
   ```bash pytest unit_tests/```
5. Registra el modelo en MLflow:
   ```bash python scripts/register_model.py```

## Variables de Entorno

- `MLFLOW_URI`: URI del servidor MLflow
- `MODEL_NAME`: Nombre del modelo a registrar en MLflow

## Notas
- Los logs de entrenamiento se guardan en `training.log`.
- El modelo y artefactos se guardan en la carpeta `models/`.

## Autor
Amalia Martín

---
Este proyecto es parte del módulo de Introducción a DevOps del Máster en IA, Cloud Computing y DevOps.
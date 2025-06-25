# Adult Income Classification Project

Este proyecto implementa un pipeline de Machine Learning para predecir si una persona gana más de 50K al año usando el dataset "Adult" del UCI Machine Learning Repository. El flujo completo incluye descarga de datos, preprocesamiento, entrenamiento, evaluación, registro del modelo en MLflow y despliegue en Azure Container Instances mediante GitHub Actions.

## Estructura del Proyecto

- **src/**: Código fuente principal
  - `main.py`: Orquestador del pipeline de entrenamiento y evaluación
  - `data_loader.py`: Carga y preprocesa los datos
  - `model.py`: Entrenamiento del modelo (RandomForestClassifier)
  - `evaluate.py`: Evaluación del modelo
- **data/raw/**: Carpeta donde se descargan los datos originales
- **models/**: Carpeta donde se guardan los modelos entrenados y artefactos
- **scripts/**: Scripts auxiliares
  - `register_model.py`: Registro del modelo entrenado en MLflow
  - `query_model.py`: Consulta del modelo desplegado
- **deployment/**: Archivos para el despliegue en Azure
  - `Dockerfile`: Imagen para servir el modelo
  - `app/`: Código de la API para inferencia
  - `requirements.txt`: Dependencias para el entorno de despliegue
- **model_tests/**: Pruebas del modelo entrenado
- **unit_tests/**: Pruebas unitarias para los módulos principales
- **.github/workflows/**: Workflows de CI/CD (build y deploy)

## Pipeline de Entrenamiento y Despliegue

1. **Descarga de datos**: Se descargan los archivos `adult.data` y `adult.test`.
2. **Carga y preprocesamiento**: Se leen los datos, se limpian, codifican las variables categóricas y se escalan las numéricas.
3. **Entrenamiento**: Se entrena un modelo RandomForestClassifier usando scikit-learn.
4. **Evaluación**: Se evalúa el modelo en el conjunto de test y se reportan métricas como accuracy y classification report.
5. **Registro**: El modelo, el scaler y los encoders se guardan y el modelo se registra en MLflow para su gestión y versionado.
6. **Despliegue**: El modelo se empaqueta en un contenedor Docker y se despliega automáticamente en Azure Container Instances usando GitHub Actions.

## Ejecución Local

1. Instala las dependencias:
   ```bash
   pip install -r requirements.txt
   ```
2. Descarga los datos en `data/raw/` desde:
   - https://archive.ics.uci.edu/ml/machine-learning-databases/adult/adult.data
   - https://archive.ics.uci.edu/ml/machine-learning-databases/adult/adult.test
3. Ejecuta el pipeline de entrenamiento:
   ```bash
   python src/main.py
   ```
4. (Opcional) Ejecuta los tests unitarios:
   ```bash
   pytest unit_tests/
   ```
5. Registra el modelo en MLflow:
   ```bash
   python scripts/register_model.py
   ```

## Despliegue Automático (CI/CD)

- El workflow `.github/workflows/build.yml` entrena y registra el modelo automáticamente al hacer push a la rama `main`.
- El workflow `.github/workflows/deploy.yml` construye la imagen Docker y despliega el modelo en Azure Container Instances.

## Variables de Entorno

- `MLFLOW_URI`: URI del servidor MLflow
- `MODEL_NAME`: Nombre del modelo a registrar y desplegar
- `AZURE_STORAGE_CONNECTION_STRING`: Conexión a Azure Blob Storage
- `ACR_NAME`, `ACR_USERNAME`, `ACR_PASSWORD`: Credenciales de Azure Container Registry
- `AZURE_RESOURCE_GROUP`: Resource group de Azure

## Notas
- Los logs de entrenamiento se guardan en `training.log`.
- El modelo y artefactos se guardan en la carpeta `models/`.
- El endpoint de salud del modelo desplegado es `/health`.

## Autor
Amalia Martín

---
Este proyecto es parte del módulo de Introducción a DevOps del Máster en IA, Cloud Computing y DevOps.
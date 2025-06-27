# Prueba Tecnica Nequi

## ☁️ Arquitectura en AWS para detección de fraccionamiento de transacciones

Esta arquitectura propone cómo escalar y desplegar la solución construida usando servicios gestionados de AWS. Se adapta a un flujo batch (diario o cada hora) y también puede escalar hacia tiempo real si se requiere.

---

### 🧩 1. Ingesta de datos

- **Amazon S3**: almacenamiento de archivos `.parquet` o `.csv` con logs de transacciones.
- *(Opcional)* **Amazon Kinesis Data Streams**: ingestión en tiempo real si se desea monitoreo online.

---

### ⚙️ 2. Procesamiento distribuido

- **AWS Glue Jobs**: ejecuta scripts de Python para calcular:
  - Ventanas móviles de 24 horas
  - Métricas como `count_amt`, `sum_amt`, `std_amt`, `delta` (tiempo entre transacciones)
- *(Alternativa)* **Amazon EMR** con Spark o Dask: si se necesita más control o procesamiento intensivo.

---

### 🤖 3. Detección de anomalías

- **Amazon SageMaker**:
  - Entrenamiento de modelos no supervisados: Isolation Forest, Local Outlier Factor (LOF), DBSCAN, Gaussian Mixture Models (GMM)
  - Implementación de lógica basada en reglas: Z-score, umbrales de conteo y suma
  - Despliegue en endpoints para inferencia periódica o por demanda

---

### 🔁 4. Orquestación

- **AWS Step Functions**:
  - Automatiza el flujo de: carga de datos → procesamiento → inferencia → guardado
- *(Alternativa)* **Amazon MWAA (Managed Workflows for Apache Airflow)**: si se prefiere usar DAGs.

---

### 💾 5. Almacenamiento de resultados

- **Amazon Redshift** o **Amazon Aurora (PostgreSQL)**:
  - Guarda resultados de ventanas flaggeadas con columnas como:
    - `user_id`, `merchant_id`, método de detección, score, fecha, etc.
- **Amazon S3**:
  - Para versionamiento y auditoría de todos los pasos del pipeline.

---

### 📊 6. Visualización y monitoreo

- **Amazon QuickSight**:
  - Dashboard de anomalías detectadas: por método, cliente, comercio, hora del día, etc.
- *(Opcional)* **Amazon Athena**:
  - Consultas ad-hoc sobre los datos en S3 (sin necesidad de moverlos).

---

### 🔐 Seguridad y monitoreo

- Roles y permisos con **IAM** para acceso restringido entre servicios
- Encriptación en tránsito (TLS) y en reposo (SSE-S3, KMS)
- Auditoría con **AWS CloudTrail**
- Logs y alertas con **Amazon CloudWatch**

---

### 🧠 Ventajas de esta arquitectura

- Escalable horizontalmente con AWS Glue y SageMaker
- Modular y reutilizable por partes
- Compatible con batch o tiempo real
- Bajo costo de mantenimiento al usar servicios serverless o gestionados

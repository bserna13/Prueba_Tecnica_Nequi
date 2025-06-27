# Prueba Tecnica Nequi

# Detección de Fraccionamiento Transaccional

Este repositorio contiene la implementación de una solución de extremo a extremo para detectar patrones de fraccionamiento de transacciones en ventanas de 24 horas. Aprovecha servicios serverless de AWS y un modelo de clustering para generar alertas casi en tiempo real.

## Contexto

En comercio electrónico y banca digital, el fraccionamiento de transacciones es una táctica común de lavado de dinero o evasión de control. Nuestra propuesta:

1. **Ingestión cada hora** de nuevos archivos de transacciones.  
2. **Feature Engineering** con ventanas móviles de 24 h (conteo, suma, media, desviación, deltas de tiempo).  
3. **Modelo de clustering** (DBSCAN/GMM) + regla heurística (> 4 tx/24 h) para clasificar comportamientos normales vs. anómalos.  
4. **Almacenamiento** de resultados horarios y batch diario de KPIs para reporting.

## Arquitectura

- **Amazon S3**: bucket `raw/transactions/`  
- **EventBridge**: dispara micro-lotes cada hora y batch diario a las 03:00 AM (Bogotá)  
- **AWS Lambda**:  
  - Orquestador horario  
  - Agregador diario  
- **AWS Glue (Spark)**: procesamiento y clustering  
- **Amazon Redshift / RDS**: tablas `alertas_horarias` y `características_horarias`  
- **Amazon QuickSight**: dashboard de alertas y tendencias  
- **SNS & CloudWatch**: notificaciones y monitoreo

## Estructura del repositorio


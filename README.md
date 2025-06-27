# Prueba Tecnica Nequi - Detección de Fraccionamiento Transaccional


Este proyecto aborda un caso realista de detección de **fraccionamiento de transacciones** dentro de una plataforma financiera, utilizando un enfoque analítico que combina reglas heurísticas, ingeniería de características y **modelos de clustering no supervisados**.

El objetivo es identificar patrones anómalos que podrían estar relacionados con prácticas fraudulentas, considerando ventanas móviles de 24 horas por usuario y comercio.

## 🛠️ ¿Qué contiene este repositorio?

Aquí encontrarás:

- Un **análisis exploratorio** de los datos, desde limpieza hasta visualización temporal.
- Implementación de **técnicas estadísticas** y reglas de negocio para detección preliminar.
- Aplicación de **modelos no supervisados** como DBSCAN y GMM para clasificar comportamientos de transacción.
- Evaluación de la distribución de patrones y agrupamientos sospechosos.
- Propuesta de una **arquitectura en AWS** para llevar el modelo a producción, con micro-lotes horarios que alimentan el sistema en casi tiempo real.

> 📝 Puedes consultar todos los pasos detallados, visualizaciones y decisiones tomadas en el notebook/documento principal que acompaña este repositorio.

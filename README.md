# UFO Data Enrichment & ETL Pipeline 🛸📊

> **Procesamiento ETL y enriquecimiento de +190k registros de avistamientos FANI/OVNI mediante Python para analítica avanzada y forecasting en SAS Viya.**

## Sobre el Proyecto
El fenómeno de los Fenómenos Anómalos No Identificados (FANI/OVNI) ha sido históricamente abordado desde lo anecdótico. Este proyecto propone un **enfoque cuantitativo y relacional**. 

Utilizando técnicas de *Data Enrichment*, cruzamos más de 190.000 reportes históricos con bases de datos meteorológicas y aeronáuticas. El objetivo no es validar el origen de los avistamientos, sino analizar el entorno estadístico en el que ocurren a través de herramientas de *Business Intelligence* (SAS Viya).

## Hipótesis de Investigación
El tablero interactivo final busca responder a las siguientes premisas:
1. **Sesgo Geográfico:** Los reportes presentan una fuerte concentración en países anglosajones y zonas de alta densidad poblacional.
2. **Morfología vs. Duración:** Existe una relación directa entre la forma del objeto reportado y su tiempo de visibilidad promedio.
3. **El Factor Climático:** La inmensa mayoría de los avistamientos ocurren bajo condiciones de cielo despejado (Clear), descartando ilusiones ópticas por nubosidad.
4. **Interferencia Aeronáutica:** Se espera encontrar una concentración estadística de casos a distancias muy cortas de aeropuertos comerciales.
5. **Estacionalidad (Forecasting):** El fenómeno presenta picos de reportes en meses de verano, permitiendo proyectar futuras "oleadas".
6. **Enfoque Local (Argentina):** Los incidentes históricos locales replican las mismas tendencias ambientales que el modelo global.

## Arquitectura de Datos (Pipeline ETL)
Para garantizar el rendimiento en la plataforma SAS Viya (límite de <100MB) y la integridad de los datos, se desarrolló un pipeline en **Python (Pandas)** con las siguientes características clave:

* **Fuzzy Matching Relacional:** Se ejecutó un `LEFT JOIN` entre el dataset ambiental (Hugging Face) y el histórico (Kaggle). Para superar las inconsistencias de segundos en los reportes, se crearon llaves sintéticas combinando la *fecha corta* y la *ciudad normalizada*, logrando una **tasa de recuperación superior al 96%** de las variables morfológicas.
* **Geographic Normalization & Sanitization:** Se aplicó un tratamiento exhaustivo de *strings* para limpiar códigos HTML (`&uacute;`) y metadatos anidados en las ubicaciones. 
* **Prevención de Falsos Positivos:** Se diseñaron máscaras de exclusión lógicas para aislar correctamente los casos de Argentina, evitando colisiones con homónimos geográficos anglosajones (ej. Santa Fe, New Mexico).

## Stack Tecnológico
* **Data Prep & ETL:** Python (Pandas)
* **Visualización & Analítica Predictiva:** SAS Viya
* **Entorno de Desarrollo:** Jupyter Notebook

## Resultados del Procesamiento
* **Volumen inicial procesado:** +320,000 registros.
* **Dataset final optimizado:** 192,777 registros íntegros (17.8 MB).
* **Nivel de completitud:** 97% de datos morfológicos rescatados.
* **Micro-análisis local:** 31 casos argentinos de alta pureza aislados para estudio de caso.

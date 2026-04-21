# UFO Data Enrichment & ETL Pipeline 🛸📊

Procesamiento ETL y enriquecimiento de más de 88.000 registros de avistamientos FANI/OVNI mediante Python para analítica avanzada y forecasting en SAS Viya.

### Sobre el Proyecto
El fenómeno de los Fenómenos Anómalos No Identificados (FANI/OVNI) ha sido históricamente abordado desde lo anecdótico. Este proyecto propone un enfoque cuantitativo y relacional.

Utilizando técnicas de Data Enrichment, cruzamos más de 327.000 reportes históricos iniciales con bases de datos meteorológicas y astronómicas. El objetivo no es validar el origen de los avistamientos, sino analizar el entorno estadístico en el que ocurren a través de herramientas de Business Intelligence (SAS Viya).

### Hipótesis de Investigación
El tablero interactivo final busca responder a las siguientes premisas:

* **Sesgo Geográfico:** Los reportes presentan una fuerte concentración en países anglosajones y zonas de alta densidad poblacional.
* **Morfología vs. Duración:** Existe una relación directa entre la forma del objeto reportado y su tiempo de visibilidad promedio.
* **El Factor Climático:** La inmensa mayoría de los avistamientos ocurren bajo condiciones de cielo despejado (*Clear*), descartando ilusiones ópticas por nubosidad.
* **Interferencia Aeronáutica:** Se espera encontrar una concentración estadística de casos a distancias muy cortas de aeropuertos comerciales.
* **Estacionalidad (Forecasting):** El fenómeno presenta picos de reportes en meses de verano, permitiendo proyectar futuras "oleadas".
* **Enfoque Local (Argentina):** Los incidentes históricos locales replican las mismas tendencias ambientales que el modelo global.

### Arquitectura de Datos (Pipeline ETL)
Para garantizar el rendimiento en la plataforma SAS Viya y la integridad de los datos, se desarrolló un pipeline en Python (Pandas) con las siguientes características clave:

* **Cruce Relacional Asincrónico (*Merge As-Of*):** Dado que los registros de segundos no coincidían exactamente entre el dataset ambiental y el histórico, se descartó un JOIN tradicional. Se implementó una unión por proximidad temporal (`merge_asof`) agrupada por ciudad, con una tolerancia de 1 minuto. Se logró una tasa de recuperación superior al 96% para las variables morfológicas rescatadas.
* **Geographic Normalization & Sanitization:** Se aplicó un tratamiento exhaustivo de strings para limpiar códigos HTML y metadatos anidados en los nombres de las ciudades.
* **Prevención de Falsos Positivos:** Se diseñaron máscaras de exclusión lógicas para aislar correctamente los casos de Argentina (`country = 'AR'`), evitando colisiones con homónimos geográficos pertenecientes a países anglosajones o al estado de New Mexico en USA.

### Stack Tecnológico
* **Data Prep & ETL:** Python (Pandas)
* **Visualización & Analítica Predictiva:** SAS Viya
* **Entorno de Desarrollo:** Jupyter Notebook

### Resultados del Procesamiento
* **Volumen inicial procesado:** 327.009 registros.
* **Dataset final optimizado:** 88.014 registros íntegros.
* **Nivel de completitud:** Tasa de recuperación >96% en las variables de forma (*shape*) y duración (*duration*).
* **Micro-análisis local:** 20 casos argentinos de alta pureza aislados y confirmados para el estudio de caso.

.

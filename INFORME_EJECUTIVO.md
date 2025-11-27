# INFORME EJECUTIVO
# Análisis del Consumo de Agua en Barcelona (2023-2024)

| **Autor** | Dragos Calin |
| :--- | :--- |
| **Fecha de Emisión** | 25 de Noviembre de 2024 |
| **Fuente de Datos** | Registros de Consumo (2023) y Alertas de Fugas (2024) |
| **Volumen Analizado** | 963,419 registros de consumo y 121,834 alertas de fugas |
| **Enfoque Técnico** | Análisis Descriptivo + ML (Clustering) + AI (Anomaly Detection) |

**[Ver análisis detallado en Jupyter Notebook](notebooks/aguas_barcelona.ipynb)**

---

## 1. Resumen Ejecutivo

Este análisis proporciona una visión estratégica del comportamiento hídrico en Barcelona, combinando estadísticas tradicionales con modelos de **Machine Learning** para identificar ineficiencias operacionales y patrones poblacionales ocultos.

El consumo de agua está altamente concentrado:
* El **52.9%** del consumo total proviene del sector **Industrial/Intensivo**. Un contador de este tipo consume **277 veces más** que uno doméstico.
* Geográficamente, los **tres distritos principales** (Sants-Montjuïc, Eixample y Ciutat Vella) concentran el **50.3%** del consumo.
* **Inteligencia de Datos:** Mediante algoritmos de Clustering, hemos identificado que la Densidad Poblacional es un factor clave de eficiencia (barrios más densos consumen menos per cápita), mientras que la Edad tiene una correlación nula (R=0.02).
* **Detección de Fraude (AI):** Un algoritmo de *Isolation Forest* ha detectado un **1% de anomalías críticas** (comportamientos matemáticamente inusuales sugestivos de fugas ocultas o fraude).
* La gestión de pérdidas muestra un punto crítico: el **24% de las fugas detectadas son reiteradas** (no reparadas con la suficiente rapidez).

---

## 2. Hallazgos Clave Detallados

### 2.1. Concentración Geográfica del Consumo

Los distritos de **Sants-Montjuïc, Eixample y Ciutat Vella** son los principales impulsores del consumo de agua en la ciudad.

| Ranking | Distrito | Consumo (Giga L/día) | % del Total |
| :---: | :--- | :---: | :---: |
| 1 | **Sants-Montjuïc** | 3.84 | 17.0% |
| 2 | **Eixample** | 3.75 | 16.6% |
| 3 | **Ciutat Vella** | 3.74 | 16.6% |

**Visualización Clave:** [Consumo por Distrito](visualizaciones/fase1c_ranking_distritos.png)

"Nota: Aunque Ciutat Vella ocupa la 3ª posición en volumen absoluto, presenta la intensidad por contador más alta de la ciudad (245 L/día), lo que indica un uso mucho más concentrado que en el Eixample (83 L/día)."

### 2.2. Segmentación Avanzada (Data Science)

Utilizando algoritmos de Machine Learning no supervisado (**K-Means**) y validación matemática (Método del Codo, K=3), hemos segmentado la ciudad en **3 perfiles estratégicos** basados en su comportamiento hídrico real (Densidad, Consumo e Industria).

**Mito de la Edad:** "El análisis descarta la edad como factor determinante (correlación espuria R=0.02). La segmentación demuestra que el consumo se explica por la estructura económica (Industria vs Turismo) y urbanística (Densidad)."

| Cluster | Perfil | Características Clave |
| :---: | :--- | :--- |
| **Rojo** | **INTENSIVO / TURÍSTICO** | **Ciutat Vella**. Distrito único con consumo per cápita extremo (**>89 L/hab**) y baja industria real. Diagnóstico: Anomalía por población flotante. |
| **Naranja** | **INDUSTRIAL** | **Sants-Montjuïc y Les Corts**. Distritos con grandes infraestructuras (Zona Franca, Camp Nou) y vocación económica (**>60% consumo industrial**). |
| **Azul** | **RESIDENCIAL COMPACTO** | **Eixample, Gràcia y resto**. La ciudad estándar: alta densidad poblacional y gran eficiencia en consumo per cápita (**<40 L/hab**). |

**Visualización Clave:** [Mapa 3D de Perfiles (Estático)](visualizaciones/fase6_clusters_3d_static.png)

### 2.3. Distribución por Tipo de Uso e Intensidad

La distribución del consumo muestra una clara dicotomía, con el sector industrial ejerciendo una presión desproporcionada sobre la red.

| Tipo de Uso | % Consumo Total | Intensidad (L/día/contador) | Contadores Estimados |
| :--- | :---: | :---: | :---: |
| **Industrial** | **52.9%** | 9,671 | **3,400** |
| Doméstico | 33.6% | 35 | 595,000 |
| Comercial | 13.5% | 135 | 61,000 |

**Visualización Clave:** [Consumo por Uso](visualizaciones/fase1a_consumo_por_uso.png)

### 2.4. Análisis de Riesgo (RCI / IIC)

El análisis de riesgo combina el Riesgo de Concentración Industrial (RCI) con la Intensidad de Consumo Industrial (IIC) para identificar áreas de intervención prioritaria.

| Distrito | RCI (Riesgo Concentración) | IIC (Intensidad L/día) | Nivel de Riesgo |
| :--- | :---: | :---: | :--- |
| **Sants-Montjuïc** | **25.6%** | 14.4k | ALTO (Concentración) |
| **Les Corts** | 10.0% | **16.2k** | ALTO (Intensidad) |
| **Eixample** | 15.1% | 9.7k | ALTO/Medio |

**Visualización Clave:** [Matriz de Riesgo](visualizaciones/fase3_matriz_riesgo.png)

### 2.5. Mapas Interactivos de Consumo

Exploración de la distribución espacial del consumo de agua en Barcelona mediante un visor GIS unificado con capas seleccionables:

| Visualización | Descripción | Enlace |
| :--- | :--- | :--- |
| **Mapa Maestro (GIS)** | Visor interactivo que permite cruzar variables clave:<br>1. **Consumo Total** (Volumen)<br>2. **% Industrial** (Actividad Económica)<br>3. **Per Cápita** (Eficiencia) | [ **Abrir Mapa Interactivo**](https://dragoscalin33.github.io/Aguas_Barcelona_Consumo_2023_2024/mapas/mapa_maestro_barcelona.html) |

### 2.6. Análisis de Fugas y Pérdidas: La Paradoja Estacional

El análisis de 121,834 alertas revela que el sistema de gestión actual es reactivo y no discrimina por impacto real.

| Métrica | Q1 (Invierno) | Q3 (Verano) | Diagnóstico |
| :--- | :---: | :---: | :--- |
| **Nº Alertas** | 41,306 | 43,756 | Volumen de avisos similar. |
| **Agua Perdida** | 0.9 Millones L | **5.0 Millones L** | **El daño se multiplica x5.** |
| **Tipo de Fuga** | Micro-fugas / Ruido | Roturas Estructurales | Prioridad crítica en Agosto. |

**Hallazgos Operativos:**
1.  **Reiteración (24%):** Una de cada cuatro reparaciones falla o se retrasa, generando duplicidad de avisos.
2.  **Puntos Ciegos (Data Quality):** El **12%** de las alertas (14,851 casos) no registran el dato de "Litros Perdidos", impidiendo su priorización automática.
3.  **Fugas "Monstruo":** Se han identificado roturas industriales de **>6,000 L/día** que conviven en la misma cola de trabajo que fugas domésticas de 20 L/día.

### 2.7. Detección de Anomalías con IA

Implementación de **Isolation Forest** para detectar patrones atípicos en el comportamiento agregado de los distritos:
* **Hallazgo:** El modelo aisló automáticamente al **Distrito 01 (Ciutat Vella)** como un *outlier* respecto al estándar de la ciudad.
* **Diagnóstico:** Mientras el resto de distritos mantienen una relación coherente entre número de contadores y volumen, Ciutat Vella presenta una **intensidad desproporcionada**, validando la necesidad de una auditoría específica en esta zona.

**Visualización Clave:** [Detección Anomalías AI](visualizaciones/fase7_anomalias_ai.png)

"El análisis detallado reveló que los contadores clasificados como 'domésticos' en Ciutat Vella consumen 4 veces más (122 L/día) que en el Eixample (28 L/día), apuntando a una alta prevalencia de pisos turísticos o actividad comercial encubierta."

---

## 3. Recomendaciones Priorizadas

Las siguientes acciones están ordenadas por potencial de ahorro a corto y medio plazo.

### PRIORIDAD 1: Auditoría en Ciutat Vella (Inmediata)
- **Acción**: Inspección técnica de la red en el Distrito 1.
- **Justificación**: Marcado como "Anomalía" por la IA debido a su intensidad desproporcionada (245 L/contador).

### PRIORIDAD 2: Plan de Choque Industrial
- **Acción**: Auditoría dirigida a **1,287 grandes contadores** estratégicos en Sants-Montjuïc, Eixample y Les Corts.
- **Impacto**: Con solo el **0.1%** de las inspecciones, se controla el **60%** del consumo industrial total.
- **Objetivo**: Recuperación estimada de **600 Millones de Litros/día** (detectando un 10% de ineficiencia).

### PRIORIDAD 3: Inspección de Fraude (IA)
- **Acción**: Revisión in-situ del 1% de anomalías detectadas por Isolation Forest.
- **Objetivo**: Recuperación de ingresos y detección de tomas ilegales.

### PRIORIDAD 4: Estrategia Segmentada por Perfiles
- **Acción**: Campañas de concienciación diferenciadas según el Cluster detectado.
    - *Cluster A (Turístico):* Control de licencias y eficiencia en hostelería.
    - *Cluster B (Residencial):* Foco en comunidades de vecinos y ahorro doméstico.

### PRIORIDAD 5: Protocolo de Calidad (Fugas Reiteradas)
- **Acción**: Implementar auditoría de calidad post-reparación y análisis de causa raíz en incidencias repetitivas.
- **Objetivo**: Reducir la tasa de reiteración del 24% a <10%.

---

## 4. Metodología y Herramientas

### 4.1. Datasets
* **Consumo (2023):** 963,419 registros que incluyen tipo de uso, distrito y volumen consumido.
* **Fugas (2024):** 121,834 alertas con información de localización, fecha y estado de reparación.
* **Datos Demográficos:** Dataset construido a partir de la agregación de fuentes oficiales:
    * *Población y Edad:* **Ajuntament de Barcelona (Open Data)** - Padrón Municipal a 1 de enero de 2024.
    * *Territorio:* **Idescat** - Superficie y densidad oficial por distrito.

### 4.2. Métricas Clave
* **RCI (Riesgo de Concentración Industrial):** Porcentaje del consumo industrial sobre el total del distrito.
* **IIC (Intensidad de Consumo Industrial):** Litros por día por contador industrial.
* **Consumo per cápita:** Litros por día por habitante.

### 4.3. Herramientas y Stack Tecnológico
* **Procesamiento:** Python, Pandas, NumPy.
* **Machine Learning & AI:**
    * **Clustering:** Scikit-learn (K-Means), validado mediante **Método del Codo** y **Silhouette Score**.
    * **Anomaly Detection:** Isolation Forest.
* **Visualización:** Matplotlib, Seaborn, Folium/GeoPandas.

---

## 5. Conclusiones

El análisis revela tres áreas críticas de intervención:

1.  **Concentración Industrial:** El sector industrial representa más de la mitad del consumo total, con distritos como Ciutat Vella mostrando intensidades extremas.
2.  **Inteligencia de Datos:** La aplicación de Data Science ha permitido segmentar la ciudad en 3 perfiles claros, identificando al Cluster A (Zona Turística) como el foco principal de intensidad de uso, desplazando el foco tradicional puramente residencial.
3.  **Ineficiencia Operativa:** Una cuarta parte de las fugas son reiteradas.

La implementación de las auditorías en Ciutat Vella y la estrategia segmentada por clusters tienen el potencial de reducir el consumo significativamente y mejorar la resiliencia del sistema hídrico.

"Nota: La metodología de detección de anomalías presentada ha sido contrastada favorablemente con expertos del sector, identificándose como futuras líneas de mejora la incorporación de variables hidráulicas (presión de red) y físicas (material de tuberías) para aumentar la precisión predictiva."

---

## Anexos y Recursos Adicionales

### A. Visualizaciones Complementarias

**1. Correlaciones Operativas**
![Mapa de Calor](visualizaciones/fase1e_mapa_calor_correlaciones.png)
* **Hallazgo:** Correlación extrema (**r=0.98**) entre intensidad técnica y consumo per cápita. También confirma la nulidad de la correlación Edad-Consumo (**r=0.02**).

**2. Composición por Distrito**
![Heatmap Composición](visualizaciones/fase2_1_heatmap_composicion.png)
* **Hallazgo:** Dicotomía clara (**r=-0.96**) entre distritos industriales y domésticos.

**3. Visualización 3D Interactiva**
* [Explorador de Clusters 3D (Archivo HTML)](visualizaciones/fase6_clusters_3d_interactivo.html) - *Requiere descarga para visualizar la interactividad.*

### B. Documentación Técnica
* **Notebook Completo:** [Análisis en Jupyter](notebooks/aguas_barcelona.ipynb)
* **Código Fuente:** Disponible en el repositorio del proyecto

### C. Contacto
Para consultas sobre este informe o acceso a los datos completos:

**Autor:** Dragos Calin  
**LinkedIn:** [linkedin.com/in/dragos-calin33](https://www.linkedin.com/in/dragos-calin33/)  
**Email:** dragoscalin@yahoo.com

---

* Este informe fue generado como parte del análisis del consumo de agua en Barcelona. 
* Todos los datos utilizados provienen de fuentes oficiales y están disponibles en el repositorio del proyecto.

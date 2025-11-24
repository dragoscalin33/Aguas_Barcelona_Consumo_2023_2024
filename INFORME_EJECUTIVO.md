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
* **Inteligencia de Datos:** Mediante algoritmos de Clustering, hemos identificado que la **Renta** es un predictor de consumo mucho más fuerte que la **Edad** (cuya correlación es casi nula, R=0.02).
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

### 2.2. Segmentación Avanzada (Data Science)

Utilizando algoritmos no supervisados (**K-Means**), hemos segmentado la población en 4 perfiles de comportamiento para personalizar las estrategias de ahorro.

* **Cluster 3 (Zona Rica - Alto Consumo):** Secciones censales con Renta media alta (~64k€) y el mayor consumo per cápita (**212 L/hab/día**). *Factor clave: Piscinas y riego.*
* **Cluster 0 (Clase Media):** Consumo moderado y demografía equilibrada.
* **Cluster 1 (Zona Envejecida):** Menor consumo per cápita asociado a hogares unipersonales.
* **Mito de la Edad:** El análisis estadístico confirma que la edad **no correlaciona** con el consumo (R=0.02); el factor determinante es el nivel socioeconómico.

**Visualización Clave:** [Perfiles de Consumo (Radar Chart)](visualizaciones/fase6_radar_chart.png)

### 2.3. Distribución por Tipo de Uso e Intensidad

La distribución del consumo muestra una clara dicotomía, con el sector industrial ejerciendo una presión desproporcionada sobre la red.

| Tipo de Uso | % Consumo Total | Intensidad (L/día/contador) | Multiplicador vs Doméstico |
| :--- | :---: | :---: | :---: |
| **Industrial** | **52.9%** | 9,671 | **277x** |
| Doméstico | 33.6% | 35 | 1x |
| Comercial | 13.5% | 135 | 3.9x |

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

Exploración la distribución espacial del consumo de agua en Barcelona mediante mapas interactivos:

| Mapa | Descripción | Enlace |
|------|-------------|--------|
| **Consumo Total** | Volumen total de agua consumida por distrito | [Ver mapa interactivo](https://dragoscalin33.github.io/Aguas_Barcelona_Consumo_2023_2024/mapas/mapa_consumo_total.html) |
| **% Industrial** | Porcentaje del consumo destinado al sector industrial | [Ver mapa interactivo](https://dragoscalin33.github.io/Aguas_Barcelona_Consumo_2023_2024/mapas/mapa_industrial.html) |
| **Per Cápita** | Consumo de agua por habitante y día | [Ver mapa interactivo](https://dragoscalin33.github.io/Aguas_Barcelona_Consumo_2023_2024/mapas/mapa_per_capita.html) |

### 2.6. Análisis de Fugas y Pérdidas

Se analizaron **121,834 alertas de fugas** registradas en 2024.

* **Fugas Reiteradas:** El **24.2%** de las alertas corresponden a fugas que ya habían sido notificadas previamente, lo que sugiere ineficiencia en el protocolo de respuesta.
* **Impacto Estacional:** El **Tercer Trimestre (Q3 - Verano)** concentra el **83%** del volumen total de consumo de fugas (5.0M L).

**Visualización Clave:** [Evolución de Fugas](visualizaciones/fase5_evolucion_fugas.png)

---

### 2.7. Detección de Anomalías con IA (Nuevo)

Implementación de **Isolation Forest** para detectar casos atípicos que escapan a las reglas simples:
* **Hallazgo:** Se ha aislado el **1%** de los contadores con comportamiento anómalo (consumo desproporcionado para su categoría).
* **Acción:** Estos casos son "Flags" automáticos para inspección prioritaria de fraude.

**Visualización Clave:** [Detección Anomalías AI](visualizaciones/fase7_anomalias_ai.png)

---

## 3. Recomendaciones Priorizadas

Las siguientes acciones están ordenadas por potencial de ahorro a corto y medio plazo.

| Prioridad | Foco | Acción Recomendada | Ahorro Potencial / Objetivo | Plazo |
| :---: | :--- | :--- | :---: | :---: |
| **1** | **Les Corts (Intensidad)** | **Auditoría Industrial:** Inspección de los 73,253 contadores industriales en Les Corts. | **119 M L/día** | 0-6 meses |
| **2** | **Fraude / Anomalías** | **Inspección IA:** Revisión in-situ del 1% de casos detectados por el algoritmo Isolation Forest. | Recuperación de Ingresos |
| **3** | **Segmentación (ML)** | **Estrategia por Perfiles:** Campañas diferenciadas (Cluster 3: Riego/Piscinas vs Cluster 0: Hogar). | Eficiencia Conductual | 3-9 meses |
| **4** | **Fugas Operacionales** | **Protocolo de Urgencia:** Reparación en <24h para fugas >100 L/día. | Reducir reiteración al <10% | Continuo |
| **4** | **Sants-Montjuïc** | **Auditoría General:** Inspección masiva por volumen total. | **305 M L/día** | 6-12 meses |

---

## 4. Metodología y Herramientas

### 4.1. Datasets
* **Consumo (2023):** 963,419 registros que incluyen tipo de uso, distrito, y volumen consumido.
* **Fugas (2024):** 121,834 alertas con información de localización, fecha, y estado de reparación.
* **Datos Demográficos:** Datos sintéticos generados basados en estadística oficial de BCN para la validación del modelo de clustering (ante restricciones de privacidad).

### 4.2. Métricas Clave
* **RCI (Riesgo de Concentración Industrial):** Porcentaje del consumo industrial sobre el total del distrito.
* **IIC (Intensidad de Consumo Industrial):** Litros por día por contador industrial.
* **Consumo per cápita:** Litros por día por habitante.

### 4.3. Herramientas y Stack Tecnológico
* **Procesamiento:** Python, Pandas, NumPy.
* * **Machine Learning & AI:** Scikit-learn (**K-Means** para clustering, **Isolation Forest** para anomalías).
* **Visualización:** Matplotlib, Seaborn, Folium/GeoPandas.

---

## 5. Conclusiones

El análisis revela tres áreas críticas de intervención:

1.  **Concentración Industrial:** El sector industrial representa más de la mitad del consumo total, con distritos como Les Corts mostrando intensidades extremas.
2.  **Inteligencia de Datos:** La aplicación de **Data Science** ha permitido desmentir mitos (la edad no afecta al consumo) y segmentar a la población rica (Cluster 3) como foco principal para políticas de ahorro en riego y piscinas.
3.  **Ineficiencia Operativa:** Una cuarta parte de las fugas son reiteradas.

La implementación de las auditorías en Les Corts y la estrategia segmentada por clusters tienen el potencial de reducir el consumo significativamente y mejorar la resiliencia del sistema hídrico.

---

## Anexos y Recursos Adicionales

### A. Visualizaciones Complementarias
* [Mapa de Calor de Correlaciones](visualizaciones/fase1e_mapa_calor_correlaciones.png)
* [Heatmap de Composición por Distrito](visualizaciones/fase2_1_heatmap_composicion.png)
* [Matriz de Correlación Demográfica](visualizaciones/fase6_mapa_correlacion.png)

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

# INFORME EJECUTIVO
# Análisis del Consumo de Agua en Barcelona (2023-2024)

| **Autor** | Dragos Calin |
| :--- | :--- |
| **Fecha de Emisión** | 25 de Noviembre de 2024 |
| **Fuente de Datos** | Registros de Consumo (2023) y Alertas de Fugas (2024) |
| **Volumen Analizado** | 963,419 registros de consumo y 121,834 alertas de fugas |

**[Ver análisis detallado en Jupyter Notebook](notebooks/aguas_barcelona.ipynb)**

---

## 1. Resumen Ejecutivo

Este análisis proporciona una visión detallada del comportamiento hídrico en Barcelona, identificando las áreas de mayor impacto y las ineficiencias operacionales.

El consumo de agua está altamente concentrado:
* El **52.9%** del consumo total proviene del sector **Industrial/Intensivo**. Un contador de este tipo consume **277 veces más** que uno doméstico.
* Geográficamente, los **tres distritos principales** (Sants-Montjuïc, Eixample y Ciutat Vella) concentran el **50.3%** del consumo.
* La gestión de pérdidas muestra un punto crítico: el **24% de las fugas detectadas son reiteradas** (no reparadas con la suficiente rapidez), lo que indica una pérdida evitable de recursos.

Las recomendaciones se centran en auditorías focalizadas en los distritos de alto riesgo (Les Corts y Sants-Montjuïc) y en la implementación de un protocolo de reparación de fugas urgente para reducir las pérdidas operacionales.

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

### 2.2. Distribución por Tipo de Uso e Intensidad

La distribución del consumo muestra una clara dicotomía, con el sector industrial ejerciendo una presión desproporcionada sobre la red.

| Tipo de Uso | % Consumo Total | Intensidad (L/día/contador) | Multiplicador vs Doméstico |
| :--- | :---: | :---: | :---: |
| **Industrial** | **52.9%** | 9,671 | **277x** |
| Doméstico | 33.6% | 35 | 1x |
| Comercial | 13.5% | 135 | 3.9x |

**Visualización Clave:** [Consumo por Uso](visualizaciones/fase1a_consumo_por_uso.png)

**Insight:** La eficiencia operativa debe centrarse en la gestión y optimización del consumo industrial.

### 2.3. Análisis de Riesgo (RCI / IIC)

El análisis de riesgo combina el Riesgo de Concentración Industrial (RCI) con la Intensidad de Consumo Industrial (IIC) para identificar áreas de intervención prioritaria.

| Distrito | RCI (Riesgo de Concentración) | IIC (Intensidad L/día/contador) | Nivel de Riesgo |
| :--- | :---: | :---: | :--- |
| **Sants-Montjuïc** | **25.6%** | 14.4k | ALTO (Concentración) |
| **Les Corts** | 10.0% | **16.2k** | ALTO (Intensidad) |
| **Eixample** | 15.1% | 9.7k | ALTO/Medio |

**Visualización Clave:** [Matriz de Riesgo](visualizaciones/fase3_matriz_riesgo.png)

### 2.4. Mapas Interactivos de Consumo por Distrito

Explore la distribución espacial del consumo de agua en Barcelona mediante mapas interactivos:

| Mapa | Descripción | Enlace |
|------|-------------|--------|
| **Consumo Total** | Volumen total de agua consumida por distrito | [Ver mapa interactivo](https://dragoscalin33.github.io/Aguas_Barcelona_Consumo_2023_2024/mapas/mapa_consumo_total.html) |
| **% Industrial** | Porcentaje del consumo destinado al sector industrial | [Ver mapa interactivo](https://dragoscalin33.github.io/Aguas_Barcelona_Consumo_2023_2024/mapas/mapa_industrial.html) |
| **Per Cápita** | Consumo de agua por habitante y día | [Ver mapa interactivo](https://dragoscalin33.github.io/Aguas_Barcelona_Consumo_2023_2024/mapas/mapa_per_capita.html) |

### 2.5. Análisis de Fugas y Pérdidas

Se analizaron **121,834 alertas de fugas** registradas en 2024.

* **Fugas Reiteradas:** El **24.2%** de las alertas corresponden a fugas que ya habían sido notificadas previamente y no se repararon a tiempo, lo que sugiere una ineficiencia en el protocolo de respuesta.
* **Impacto Estacional:** El **Tercer Trimestre (Q3)** concentra el **83%** del volumen total de consumo de fugas (5.0M L), indicando que, si bien el número de fugas es constante, las fugas de alto volumen son principalmente estacionales.

**Visualización Clave:** [Evolución de Fugas](visualizaciones/fase5_evolucion_fugas.png)

---

## 3. Recomendaciones Priorizadas

Las siguientes acciones están ordenadas por potencial de ahorro a corto y medio plazo, y por la corrección de ineficiencias operacionales.

| Prioridad | Foco | Acción Recomendada | Ahorro Potencial Estimado | Plazo |
| :---: | :--- | :--- | :---: | :---: |
| **1** | **Les Corts (Intensidad)** | **Auditoría Intensiva:** Inspección de los 73,253 contadores industriales en Les Corts para identificar consumos anómalos y oportunidades de optimización. | **119 M L/día** | 0-6 meses |
| **2** | **Fugas Operacionales** | **Protocolo de Urgencia:** Reparación en menos de 24 horas para fugas con un consumo registrado superior a 100 L/día. Objetivo: Reducir la tasa de reiteración de 24% a <10%. | Reducción significativa de pérdidas operativas | Continuo |
| **3** | **Sants-Montjuïc (Concentración)** | **Auditoría General:** Inspección de los 211,859 contadores del distrito con mayor consumo total para identificar ineficiencias y consumos irregulares. | **305 M L/día** | 6-12 meses |

---

## 4. Metodología y Herramientas

### 4.1. Datasets
* **Consumo (2023):** 963,419 registros que incluyen tipo de uso, distrito, y volumen consumido.
* **Fugas (2024):** 121,834 alertas con información de localización, fecha, y estado de reparación.

### 4.2. Métricas Clave
* **RCI (Riesgo de Concentración Industrial):** Porcentaje del consumo industrial sobre el total del distrito.
* **IIC (Intensidad de Consumo Industrial):** Litros por día por contador industrial.
* **Consumo per cápita:** Litros por día por habitante.
* **Tasa de Reiteración de Fugas:** Porcentaje de fugas que no fueron reparadas en el primer reporte.

### 4.3. Herramientas
El análisis se realizó utilizando Python y las siguientes librerías especializadas:
* **Pandas:** Manipulación y análisis de datos
* **Matplotlib/Seaborn:** Visualización estática y análisis exploratorio
* **Folium/GeoPandas:** Mapas interactivos y análisis geoespacial

---

## 5. Conclusiones

El análisis revela tres áreas críticas de intervención:

1. **Concentración Industrial:** El sector industrial representa más de la mitad del consumo total, con distritos como Les Corts mostrando intensidades extremadamente altas (16.2k L/día por contador).

2. **Ineficiencia en Gestión de Fugas:** Una cuarta parte de las fugas son reiteradas, lo que indica un problema sistemático en los protocolos de reparación que genera pérdidas evitables.

3. **Oportunidades de Ahorro Significativas:** Las auditorías focalizadas en Les Corts y Sants-Montjuïc tienen el potencial de reducir el consumo en más de 400M L/día, equivalente al consumo diario de aproximadamente 11 millones de personas con estándares domésticos.

La implementación de las recomendaciones priorizadas permitirá no solo reducir el consumo y las pérdidas, sino también mejorar la resiliencia del sistema hídrico de Barcelona frente a escenarios de escasez.

---

## Anexos y Recursos Adicionales

### A. Visualizaciones Complementarias
* [Mapa de Calor de Correlaciones](visualizaciones/fase1e_mapa_calor_correlaciones.png)
* [Heatmap de Composición por Distrito](visualizaciones/fase2_1_heatmap_composicion.png)

### B. Documentación Técnica
* **Notebook Completo:** [Análisis en Jupyter](notebooks/aguas_barcelona.ipynb)
* **Código Fuente:** Disponible en el repositorio del proyecto

### C. Contacto
Para consultas sobre este informe o acceso a los datos completos:

**Autor:** Dragos Calin  
**LinkedIn:** [linkedin.com/in/dragos-calin33](https://www.linkedin.com/in/dragos-calin33/)  
**Email:** dragoscalin@yahoo.com

---

*Este informe fue generado como parte del análisis del consumo de agua en Barcelona. Todos los datos utilizados provienen de fuentes oficiales y están disponibles en el repositorio del proyecto.*

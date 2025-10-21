# Análisis del Consumo de Agua en Barcelona (2023-2024)

Análisis exhaustivo de 963,419 registros de consumo de agua y 121,834 alertas de fugas en Barcelona, identificando patrones de consumo, distritos críticos y oportunidades de ahorro.

---

## Resumen Ejecutivo

- **52.9%** del consumo es industrial/intensivo
- **Top 3 distritos** concentran el **50.3%** del consumo total
- **Sants-Montjuïc** representa el **25.6%** del consumo industrial
- **24%** de fugas son reiteradas (no reparadas a tiempo)

---

## Hallazgos Clave

### 1. Concentración Geográfica

![Consumo por Distrito](visualizaciones/fase1c_ranking_distritos.png)

**Top 3 distritos críticos:**
1. **Sants-Montjuïc**: 3.84 Giga L/día (17.0%)
2. **Eixample**: 3.75 Giga L/día (16.6%)
3. **Ciutat Vella**: 3.74 Giga L/día (16.6%)

---

### 2. Distribución por Tipo de Uso

![Consumo por Uso](visualizaciones/fase1a_consumo_por_uso.png)

| Tipo | % Consumo | Intensidad |
|------|-----------|------------|
| Industrial | 52.9% | 9,671 L/día/contador |
| Doméstico | 33.6% | 35 L/día/contador |
| Comercial | 13.5% | 135 L/día/contador |

**Insight:** Un contador industrial consume **277× más** que uno doméstico.

---

### 3. Análisis de Riesgo (RCI/IIC)

![Matriz de Riesgo](visualizaciones/fase3_matriz_riesgo.png)

**Distritos de ALTO riesgo:**
- **Sants-Montjuïc**: RCI 25.6%, IIC 14.4k L/día
- **Les Corts**: RCI 10.0%, IIC 16.2k L/día
- **Eixample**: RCI 15.1%, IIC 9.7k L/día

---

### 4. Mapas Interactivos

Explora los mapas interactivos:

| Mapa | Vista Previa | Enlace |
|------|--------------|--------|
| **Consumo Total** | ![](visualizaciones/mapa_consumo_total_screenshot.png) | [Ver mapa interactivo](mapas/mapa_consumo_total.html) |
| **% Industrial** | ![](visualizaciones/mapa_industrial_screenshot.png) | [Ver mapa interactivo](mapas/mapa_industrial.html) |
| **Per Cápita** | ![](visualizaciones/mapa_per_capita_screenshot.png) | [Ver mapa interactivo](mapas/mapa_per_capita.html) |

---

### 5. Análisis de Fugas

![Evolución de Fugas](visualizaciones/fase5_evolucion_fugas.png)

- **121,834 alertas** en 2024
- **75.8%** fugas nuevas, **24.2%** reiteradas
- **Q3** concentra **83%** del consumo de fugas (5.0M L)

---

## Recomendaciones Priorizadas

### PRIORIDAD 1: Auditoría en Les Corts (0-6 meses)
- **Acción**: Inspección de 73,253 contadores industriales
- **Ahorro Potencial**: 119M L/día

### PRIORIDAD 2: Protocolo Fugas Reiteradas
- **Acción**: Reparación <24h para fugas >100 L/día
- **Objetivo**: Reducir reiteración de 24% a <10%

### PRIORIDAD 3: Auditoría en Sants-Montjuïc (6-12 meses)
- **Acción**: Inspección de 211,859 contadores
- **Ahorro Potencial**: 305M L/día

---

## Metodología

- **Datasets**: 963,419 registros consumo (2023) + 121,834 alertas fugas (2024)
- **Herramientas**: Python, Pandas, Matplotlib, Seaborn, Folium, GeoPandas
- **Métricas**:
  - **RCI**: Riesgo de Concentración Industrial
  - **IIC**: Intensidad de Consumo Industrial
  - **Consumo per cápita**: L/día por habitante

📄 **[Ver Informe Ejecutivo Completo](INFORME_EJECUTIVO.md)**

---

## Estructura del Proyecto
```
📁 Analisis-Consumo-Agua-Barcelona/
├── 📄 README.md (este archivo)
├── 📄 INFORME_EJECUTIVO.md (informe completo)
├── 📁 notebooks/ (código Jupyter)
├── 📁 data/ (datasets originales)
├── 📁 mapas/ (mapas HTML interactivos)
├── 📁 visualizaciones/ (gráficos PNG)
└── 📁 resultados/ (tablas resumen)
```

---

## Visualizaciones Adicionales

### Correlaciones Clave

![Mapa de Calor](visualizaciones/fase1e_mapa_calor_correlaciones.png)

**Hallazgo:** Correlación **r=0.98** entre intensidad de contador y consumo per cápita.

### Composición por Distrito

![Heatmap Composición](visualizaciones/fase2_1_heatmap_composicion.png)

**Hallazgo:** Dicotomía clara (r=-0.96) entre distritos industriales y domésticos.

---

## Contacto

**Autor**: [Tu Nombre]  
**LinkedIn**: [tu-linkedin]  
**Email**: tu@email.com

---

## Licencia

Este proyecto está bajo licencia MIT. Ver [LICENSE](LICENSE) para más detalles.

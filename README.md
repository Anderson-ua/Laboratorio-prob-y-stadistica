# Análisis descriptivo de métricas de DevOps

Análisis de integridad de datos y estadística descriptiva sobre 5000
despliegues: duración de build/deploy, líneas modificadas, bugs, cobertura
de pruebas, tiempo de resolución de tickets, equipo, módulo, prioridad y
estado del despliegue.

## Estructura del proyecto

```
.
├── devops_metrics_5000.csv     # datos
├── analisis_devops_metrics.R   # script paso a paso (limpieza, EDA, gráficos)
├── reporte_devops.Rmd          # reporte reproducible (código + resultados + narrativa)
└── README.md
```

## Requisitos

- R (≥ 4.0) y RStudio
- Paquetes: `tidyverse`, `moments`, `knitr`, `rmarkdown`

```r
install.packages(c("tidyverse", "moments", "knitr", "rmarkdown"))
```

## Cómo ejecutar

1. Colocar `devops_metrics_5000.csv` en la misma carpeta que los archivos `.R` / `.Rmd`.
2. Abrir la carpeta como proyecto en RStudio (`File > New Project > Existing Directory`).
3. **Para explorar paso a paso y ver los gráficos en el panel *Plots*:**
   abrir `analisis_devops_metrics.R` y ejecutar todo con `Ctrl/Cmd + Alt + R`
   (o el botón *Source*).
4. **Para generar el reporte final:**
   abrir `reporte_devops.Rmd` y presionar el botón **Knit** (o `Ctrl/Cmd + Shift + K`).
   Esto genera `reporte_devops.html` con todo el análisis, tablas y gráficos
   integrados, reproducible de principio a fin.

## Contenido del análisis

1. Importación, inspección e integridad de los datos (tipos, faltantes, rangos lógicos).
2. Estadística descriptiva univariada: tendencia central, dispersión y forma (asimetría/curtosis).
3. Frecuencias y agrupación en clases de Sturges; clase modal.
4. Comparación de métricas por equipo, módulo y prioridad.
5. Relaciones bivariadas: correlaciones entre cuantitativas y tablas de contingencia entre cualitativas.
6. Visualización: histograma, boxplot, gráfico de barras y dispersión.

## Principales hallazgos

- Sin duplicados, sin valores faltantes y sin valores fuera de rango lógico.
- `commit_size_loc`, `num_bugs` y `ticket_resolution_h` presentan asimetría
  positiva marcada (cola derecha larga); el resto de las variables
  cuantitativas son aproximadamente simétricas.
- El **módulo** explica más diferencias en tasa de fallos que el **equipo**
  (`ui` y `notifications` concentran más fallos; `infra` y `database` son
  los más estables).
- La **prioridad** reduce el tiempo de resolución de tickets de forma
  consistente, pero no está asociada a una mayor tasa real de fallos.
- Las correlaciones entre variables cuantitativas son en general débiles
  (< 0.35), evidencia de que ninguna variable por sí sola explica bien a otra.

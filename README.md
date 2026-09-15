# Análisis de Mercado de Leche — FAB3

**Autor:** Emilio Lopez (A01711977)
**Archivo:** `E1_Emilio Lopez_A01711977.ipynb`

## Descripción

Notebook de análisis descriptivo y modelado de regresión sobre datos históricos de ventas de leche por fabricante (FAB1–FAB6), con foco en el desempeño del FAB3. Incluye limpieza de datos, análisis de cuota de mercado, correlaciones, y modelos de elasticidad precio-demanda.

## Datos

- **Archivo de entrada:** `Data Ventas - Gpo 601.xlsx`
- **Contenido:** ventas semanales por producto/fabricante (2022–2025), incluyendo venta en valor, litros, paquetes y precios unitarios.
- El notebook espera este archivo en la misma carpeta (ruta hardcodeada en la primera celda de código; ajustar `file_path` si se mueve el archivo).

## Requisitos

```
pandas
numpy
matplotlib
statsmodels
openpyxl   # para leer el .xlsx
```

## Estructura del notebook

### Parte 1 — Data wrangling y entendimiento de datos
1. Carga y limpieza: nulos, duplicados (ID↔producto), duplicados semanales (colapsados con verificación de totales), valores negativos.
2. **Objetivo 1:** cuota de mercado por fabricante y año, desempeño de ventas y precios en el tiempo, y análisis de Pareto (fabricantes que concentran el 80% del mercado en los últimos 12 meses).
3. **Objetivo 2:** análisis de correlación entre variables numéricas, con foco en precio vs. volumen.

### Parte 2 — Modelado
4. **Punto 3:** regresión log-log de elasticidad precio-demanda para el producto top del FAB3 (solo precio como regresor).
5. **Punto 4:** propuesta de diseño para incorporar elasticidad cruzada, estacionalidad y tendencia (sin correr el modelo).
6. **Punto 5:** modelo ampliado con tendencia, estacionalidad (trimestre) y control por longitud del mes; comparación con el modelo simple del punto 3; errores estándar HAC.
7. **Punto 6:** propuesta de modelos (Random Forest / Gradient Boosting) para pronosticar precio y ventas a 24 meses.

## Cómo correrlo

1. Colocar `Data Ventas - Gpo 601.xlsx` en la misma carpeta que el notebook (o actualizar la ruta en la primera celda).
2. Ejecutar las celdas en orden — el notebook es secuencial (las celdas de modelado dependen de los DataFrames construidos en la limpieza).

## Hallazgos principales

- **Cuota de mercado (últimos 12 meses):** FAB1 (35.9%), FAB3 (28.7%) y FAB5 (22.0%) concentran el 86.6% del mercado (análisis de Pareto).
- **Producto top FAB3:** `FAB3_1L Ent Entera`.
- **Elasticidad precio (modelo simple, solo precio):** -1.77 (demanda elástica), R² = 0.323.
- **Elasticidad precio (modelo ampliado, con tendencia + trimestre + control de semanas del mes):** -2.46, R² ajustado = 0.583. La tendencia deja de ser significativa una vez controlado el número de semanas por mes.

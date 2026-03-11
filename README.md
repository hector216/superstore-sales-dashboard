# 📊 Dashboard de Ventas - Retail (Superstore)

## Descripción

Dashboard interactivo de análisis de ventas para una cadena de retail, construido con Power BI y DAX. El proyecto analiza datos de ventas del periodo 2014-2017, proporcionando insights sobre rendimiento comercial, tendencias temporales y productos más vendidos.

## 📸 Vista previa

> ![Dashboard Preview](images/Dasboard%20SalesStore.png)

## 🎯 Objetivo

Crear un dashboard ejecutivo que permita monitorear los principales indicadores de negocio de una operación retail, identificar tendencias de crecimiento y detectar oportunidades de mejora en la rentabilidad.

## 📈 KPIs e Indicadores

| Indicador | Descripción |
|---|---|
| **Ventas** | Valor total de ventas con formato abreviado (M, K) |
| **Ganancia** | Utilidad total del periodo |
| **Margen** | Porcentaje de rentabilidad sobre ventas |
| **Órdenes** | Cantidad total de órdenes procesadas |
| **Ticket Promedio** | Valor promedio por orden |
| **Variación vs AA** | Comparativo porcentual contra el año anterior (Ventas y Ganancia) |

## 🔍 Análisis incluidos

- **Análisis de ventas y tendencias:** Evolución mensual de ventas a lo largo del periodo 2014-2017, identificando estacionalidad y patrones de crecimiento.
- **Comparativo vs año anterior:** Línea de tendencia que contrasta ventas actuales contra el mismo periodo del año anterior, con indicadores de variación porcentual (▲/▼) en las tarjetas KPI.
- **Top productos más vendidos:** Ranking de los 5 productos con mayor volumen de ventas.
- **Análisis de rentabilidad:** Margen de ganancia general para evaluar la salud financiera de la operación.
- **Ticket promedio y órdenes:** Métricas complementarias que permiten entender el comportamiento del consumidor.

## 🛠️ Herramientas utilizadas

- **Power BI Desktop** — Modelado de datos, visualización y diseño del dashboard
- **DAX (Data Analysis Expressions)** — Medidas calculadas para KPIs, formatos personalizados y comparativos YoY
- **Power Query** — Transformación y limpieza de datos (ajuste de tipos de dato, configuración regional de fechas)

## 📂 Estructura del repositorio

```
📁 superstore-sales-dashboard/
├── 📄 README.md                  ← Este archivo
├── 📁 dashboard/
│   └── Dashboard_Ventas.pbix     ← Archivo de Power BI
├── 📁 data/
│   └── superstore_dataset.csv    ← Dataset original
├── 📁 images/
│   └── dashboard_preview.png     ← Captura del dashboard
└── 📁 docs/
    └── medidas_dax.md            ← Documentación de medidas DAX
```

## 📐 Medidas DAX destacadas

### Formato de valores abreviados (M, K)
```dax
Ventas Formato = 
VAR Valor = SUM(Sales[Sales])
RETURN
    SWITCH(
        TRUE(),
        ABS(Valor) >= 1000000,
            FORMAT(Valor / 1000000, "#,0.00") & " M",
        ABS(Valor) >= 1000,
            FORMAT(Valor / 1000, "#,0.00") & " K",
        FORMAT(Valor, "#,0.00")
    )
```

### Variación porcentual vs año anterior
```dax
Var % Ventas AA = 
VAR VentasActual = SUM(Superstore[Sales])
VAR VentasAA = CALCULATE(
    SUM(Superstore[Sales]),
    SAMEPERIODLASTYEAR('Calendar'[Date])
)
RETURN
    IF(
        NOT ISBLANK(VentasAA),
        DIVIDE(VentasActual - VentasAA, VentasAA, 0),
        BLANK()
    )
```

### Indicador visual con flechas
```dax
Var Ventas Indicador = 
VAR Variacion = [Var % Ventas AA]
RETURN
    IF(
        NOT ISBLANK(Variacion),
        IF(Variacion >= 0, "▲ ", "▼ ") & FORMAT(ABS(Variacion), "0.0%") & " vs AA",
        ""
    )
```

## 📊 Fuente de datos

- **Dataset:** Superstore Dataset (Final)
- **Origen:** [Kaggle - Superstore Dataset](https://www.kaggle.com/datasets/vivek468/superstore-dataset-final)
- **Registros:** ~10,000 transacciones
- **Periodo:** Enero 2014 - Diciembre 2017
- **Campos principales:** Order Date, Sales, Profit, Quantity, Discount, Product Name, Category, Region, entre otros.

## 💡 Hallazgos clave

- Las ventas muestran un crecimiento del **46.9%** respecto al año anterior.
- La ganancia creció un **48.4%** vs el año anterior, indicando mejora en rentabilidad.
- El margen general se mantiene en **12.47%**.
- Se identifica estacionalidad con picos de ventas en los últimos meses de cada año.

## 🚀 Cómo usar este proyecto

1. Descarga el archivo `Dashboard_Ventas.pbix` de la carpeta `dashboard/`.
2. Ábrelo con Power BI Desktop (versión gratuita).
3. Los datos ya están incluidos dentro del archivo .pbix.
4. Usa el filtro de fechas para explorar diferentes periodos.

## 👤 Autor

**Héctor** — Ingeniero en Logística | Analista de datos

- LinkedIn: *(agrega tu enlace)*
- GitHub: *(agrega tu enlace)*

---

⭐ Si este proyecto te resultó útil, no dudes en darle una estrella al repositorio.

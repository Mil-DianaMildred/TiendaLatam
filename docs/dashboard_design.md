# Diseño del Dashboard — TiendaLatam

Dashboard operativo en Looker Studio (6 páginas) organizado por dominio de dato. Cada página agrupa visualizaciones de un mismo dominio; los filtros globales permiten responder múltiples preguntas sin cambiar de página.

**Prerequisito:** haber ejecutado `sql/setup_views.sql` en BigQuery. Las 9 vistas son las únicas fuentes que conecta el dashboard.

---

## 1. Fuentes de datos a conectar

En Looker Studio → **Crear → Fuente de datos → BigQuery → tiendalatam-casestudy → tiendalatam → selecciona la vista**.

| Vista | Páginas que la usan | Para qué |
|-------|---------------------|----------|
| `v_orders_enriched` | Todas | KPIs operativos, filtros globales |
| `v_monthly_metrics` | 1, 2, 6 | Revenue mensual, nuevo vs recurrente, MoM |
| `v_executive_health` | 1, 2, 3, 5, 6 | Scorecards (churn, champions %, métricas operativas) |
| `v_country_clienttype_performance` | 1, 3 | Revenue por país, madurez de mercado |
| `v_rfm_segments` | 5, 6 | Segmentos RFM, At Risk, distribución de clientes |
| `v_cohort_retention` | 6 | Heatmap de retención por cohorte |
| `v_abc_classification` | 4 | Clasificación A/B/C por producto |
| `v_stock_alerts` | 4 | Scatter stock vs ventas, alertas de inventario |
| `v_order_lines` | 4 | Treemap categoría → producto |

---

## 2. Paleta de colores

Aplicar desde Tema y diseño → Personalizar. Define la paleta en la primera página y guarda como tema predeterminado.

|Elemento                |Hex      |Uso                                                              |
|------------------------|---------|-----------------------------------------------------------------|
|Fondo                   |`#F6F8FE`|Fondo cálido y neutro para todas las páginas                     |
|Acento principal        |`#052DA6`|Headers, scorecards positivos, botones primarios                 |
|Acento secundario       |`#74ACDF`|Tarjetas secundarias, bordes, tabs activos/hover                 |
|Éxito / positivo        |`#4CAF7A`|Flechas de crecimiento, "Stock OK"                               |
|Alerta / negativo       |`#D50E35`|Flechas de caída, "Riesgo de quiebre", badges de error           |
|Alerta media / warning  |`#FDD315`|Alertas de riesgo moderado, "Revisar pronto"                     |
|Texto principal         |`#2D2D2D`|Títulos y etiquetas                                              |
|Texto sobre fondo oscuro|`#FFFFFF`|Texto en headers y componentes con `#052DA6`                     |

---

## 3. Campos calculados en Looker Studio

Crear en la fuente indicada. En Looker Studio: editar fuente de datos → **Agregar un campo**.

**En `v_orders_enriched`:**

`revenue` ya está calculado en la vista — usar directamente `SUM(revenue)`. No crear campo calculado.
`total_amount` contiene el GMV bruto (todas las órdenes); usarlo solo cuando se quiera comparar GMV vs revenue.

```
% Entregado
= SUM(is_delivered) / COUNT(order_id)

% Cancelado
= SUM(is_cancelled) / COUNT(order_id)

% Devuelto
= SUM(is_returned) / COUNT(order_id)

% En proceso (Pendiente + Procesando)
= SUM(is_in_progress) / COUNT(order_id)
```

Lo mismo aplica a `v_order_lines`: usar `SUM(revenue)` para revenue real, `SUM(line_total)` para GMV bruto por línea.

**En `v_monthly_metrics`:**

```
% Revenue Recurrente
= recurring_client_revenue / revenue
```

**En `v_rfm_segments`:**

```
Es Champion
= CASE WHEN segment = "Champions" THEN 1 ELSE 0 END

Es At Risk o Hibernating
= CASE WHEN segment IN ("At Risk", "Hibernating") THEN 1 ELSE 0 END
```

---

## 4. Estructura de las 6 páginas

### Página 1 — Overview

```
┌──────────────────────────────────────────────────────────────────┐
│ Overview                 [Fecha] [País] [Tipo cliente]           │
├────────────┬────────────┬────────────┬────────────┬─────────────┤
│  Revenue   │    AOV     │  Clientes  │  Churn     │  % Revenue  │
│  total     │            │  activos   │  180d      │  recurrente │
│ (vs per.   │ (vs per.   │ (vs per.   │            │             │
│  anterior) │  anterior) │  anterior) │            │             │
├────────────┴────────────┴────────────┴────────────┴─────────────┤
│ Revenue mensual                                                   │
│ Fuente: v_monthly_metrics · dimensión: month · métrica: revenue  │
├───────────────────────────────┬──────────────────────────────────┤
│ Revenue por país              │ Distribución de estados          │
│ Mapa geográfico LATAM         │ de órdenes — donut               │
│ Fuente: v_country_clienttype_performance │ Fuente: v_orders_enriched        │
│ métrica: revenue              │ dimensión: order_status          │
│                               │ métrica: COUNT(order_id)         │
└───────────────────────────────┴──────────────────────────────────┘
```

**Configuración:**
- Scorecards (fila superior): fuente `v_executive_health`. Activar "Comparación con período anterior" en Revenue, AOV y Clientes activos.
- Revenue mensual: fuente `v_monthly_metrics`, dimensión `month`, métrica `revenue`. Gráfico de línea simple.
- Mapa: fuente `v_country_clienttype_performance`, dimensión `country` (tipo Geo → País), métrica `revenue`. Gradiente de color desde el acento secundario al acento principal.
- Donut de estados: fuente `v_orders_enriched`, dimensión `order_status`, métrica `COUNT(order_id)`. Colores: Entregado = `#4CAF7A`, Enviado = `#74ACDF`, Pendiente/Procesando = `#FDD315`, Cancelado/Devuelto = `#D50E35`.

---

### Página 2 — Revenue & Finance

```
┌──────────────────────────────────────────────────────────────────┐
│ Revenue & Finance        [Fecha] [País] [Tipo cliente]           │
├────────────────┬────────────────┬───────────────┬───────────────┤
│  Revenue       │  Crecimiento   │  AOV          │  % Revenue    │
│  del período   │  MoM           │               │  recurrente   │
│ (vs per. ant.) │ (vs per. ant.) │ (vs per. ant.)│               │
├────────────────┴────────────────┴───────────────┴───────────────┤
│ Revenue mensual nuevo vs recurrente — barras apiladas            │
│ Fuente: v_monthly_metrics                                        │
│ dimensión: month · métricas: new_client_revenue +                │
│ recurring_client_revenue                                         │
├──────────────────────────────────┬───────────────────────────────┤
│ Revenue por país — barras        │ AOV por tipo de cliente       │
│ horizontales                     │ por trimestre — líneas        │
│ Fuente: v_country_clienttype_performance    │ Fuente: v_orders_enriched     │
│ dimensión: country               │ dimensión: DATE_TRUNC(        │
│ métrica: revenue · orden desc    │   registration_date, QUARTER) │
│                                  │ series: client_type           │
│                                  │ métrica: AVG(total_amount)    │
│                                  │ filtro: status IN (3,4)       │
└──────────────────────────────────┴───────────────────────────────┘
```

**Configuración:**
- Scorecard Revenue del período: fuente `v_monthly_metrics`, métrica `revenue`. Activar comparación con período anterior.
- Scorecard Crecimiento MoM: fuente `v_monthly_metrics`, métrica `mom_growth_pct`. Activar comparación con período anterior.
- Scorecard AOV: fuente v_orders_enriched, métrica AVG(total_amount), filtro is_valid_revenue = 1. Activar comparación con período anterior.
- Scorecard % Revenue Recurrente: fuente `v_monthly_metrics`, campo calculado `% Revenue Recurrente`.
- Barras apiladas: fuente `v_monthly_metrics`. Serie 1 = `new_client_revenue` (acento secundario `#74ACDF`), serie 2 = `recurring_client_revenue` (acento principal `#052DA6`).
- Barras de revenue por país: fuente `v_country_clienttype_performance`, dimensión `country`, métrica `revenue`. Ordenar descendente.
- Líneas de AOV por tipo: fuente `v_orders_enriched` con filtro `order_status_id IN (3, 4)`. Dimensión de tiempo = `DATE_TRUNC(registration_date, QUARTER)`, series = `client_type`, métrica = `AVG(total_amount)`.

---

### Página 3 — Orders & Operations

```
┌──────────────────────────────────────────────────────────────────┐
│ Orders & Operations      [Fecha] [País] [Tipo cliente]           │
├────────────────┬─────────────────┬──────────────┬───────────────┤
│  % Entregado   │  % En proceso   │  % Cancelado │  % Devuelto   │
├────────────────┴─────────────────┴──────────────┴───────────────┤
│ Performance operativa por país — tabla con color condicional      │
│ columnas: país | meses activo | revenue | revenue/mes | AOV      │
│           | % entregado | % cancelado | % devuelto               │
│ Fuente: v_country_clienttype_performance · ordenar por revenue desc         │
│ Color condicional en % cancelado y % devuelto                    │
├──────────────────────────────────┬───────────────────────────────┤
│ Revenue/mes activo vs tasa de    │ Órdenes mensuales por país    │
│ cancelación — scatter            │ barras apiladas               │
│ Fuente: v_country_clienttype_performance    │ Fuente: v_orders_enriched     │
│ X: pct_cancelled                 │ dimensión: month + country    │
│ Y: revenue_per_month_active      │ métrica: COUNT(order_id)      │
│ etiqueta: country                │                               │
└──────────────────────────────────┴───────────────────────────────┘
```

**Configuración:**
- Scorecards: fuente `v_executive_health`. Los campos `pct_delivered`, `pct_in_progress`, `pct_cancelled`, `pct_returned` ya están calculados en la vista.

- Tabla de países: fuente `v_country_clienttype_performance`. Activar "Barra de datos" en `revenue` y "Escala de color" en `pct_cancelled` y `pct_returned`. Valores altos en alerta negativa (`#D50E35`), valores bajos en éxito (`#4CAF7A`).

- Scatter: fuente `v_country_clienttype_performance`. Eje X = `pct_cancelled`, eje Y = `revenue_per_month_active`, etiqueta = `country`. Añadir líneas de referencia en los promedios de ambos ejes para delimitar cuadrantes.
- Barras apiladas de órdenes por país: fuente `v_orders_enriched`, dimensión `month` + series `country`, métrica `COUNT(order_id)`.

---

### Página 4 — Products & Catalog

```
┌──────────────────────────────────────────────────────────────────┐
│ Products & Catalog       [Fecha] [País] [Tipo cliente]           │
├──────────────────────────────┬───────────────────────────────────┤ 
│ Treemap categoría → producto │ Revenue por categoría — barras    │
│ Fuente: v_order_lines        │ Fuente: v_order_lines             │
│ filtro: status IN (3,4)      │ filtro: status IN (3,4)           │
│ dim: category → product_name │ dimensión: category               │
│ métrica: SUM(line_total)     │ métrica: SUM(line_total)          │
├──────────────────────────────┴───────────────────────────────────┤
│ Clasificación ABC de productos — tabla con color condicional      │
│ columnas: producto | categoría | revenue | % revenue             │
│           | % acumulado | clase ABC | precio lista | stock       │
│ Fuente: v_abc_classification                                      │
│ Color: A = #4CAF7A · B = #FDD315 · C = gris neutro              │
├──────────────────────────────────┬───────────────────────────────┤
│ Stock vs ventas 90d — scatter    │ Alertas de inventario — tabla │
│ Fuente: v_stock_alerts           │ Fuente: v_stock_alerts        │
│ X: stock                         │ filtro: stock_alert =         │
│ Y: units_sold_last_90d           │ 'Riesgo de quiebre'           │
│ color: stock_alert               │ columnas: producto | stock |  │
│ etiqueta: product_name           │ días inventario | alerta      │
│                                  │ orden: days_of_inventory asc  │
└──────────────────────────────────┴───────────────────────────────┘
```

**Configuración:**
- Treemap: fuente `v_order_lines` con filtro `order_status_id IN (3, 4)`. Dimensión nivel 1 = `category`, nivel 2 = `product_name`. Métrica = `SUM(line_total)`. Activar etiquetas con porcentaje.
- Barras de revenue por categoría: fuente `v_order_lines` con filtro `order_status_id IN (3, 4)`. Dimensión `category`, métrica `SUM(line_total)`. Ordenar descendente.
- Tabla ABC: fuente `v_abc_classification`. Color condicional por `abc_class`: A = fondo `#4CAF7A`, B = `#FDD315`, C = gris neutro.
- Scatter de stock: fuente `v_stock_alerts`. Color del punto: `stock_alert = "Riesgo de quiebre"` → `#D50E35`, `"Stock OK"` → `#4CAF7A`. Etiqueta = `product_name`.
- Tabla de alertas: fuente `v_stock_alerts` con filtro `stock_alert = "Riesgo de quiebre"`. Ordenada por `days_of_inventory` ascendente.

---

### Página 5 — Customers

```
┌──────────────────────────────────────────────────────────────────┐
│ Customers                [Fecha] [País] [Tipo cliente]           │
├────────────┬─────────────┬─────────────┬───────────┬────────────┤
│  Clientes  │  Nuevos     │  Recurrentes│  Churn    │  AOV       │
│  activos   │  (período)  │  (período)  │  180d     │            │
├────────────┴─────────────┴──────────┬──┴───────────┴────────────┤
│ Revenue por segmento RFM            │ Distribución de clientes   │
│ barras horizontales                 │ por segmento — donut       │
│ Fuente: v_rfm_segments              │ Fuente: v_rfm_segments     │
│ dimensión: segment                  │ dimensión: segment         │
│ métrica: SUM(monetary)              │ métrica: COUNT(client_id)  │
├─────────────────────────────────────┴────────────────────────────┤
│ Clientes At Risk / Hibernating — tabla exportable                 │
│ Fuente: v_rfm_segments                                           │
│ filtro: segment IN ('At Risk', 'Hibernating')                    │
│ columnas: client_name | country | monetary | recency_days        │
│           | segment · orden: monetary desc                       │
└──────────────────────────────────────────────────────────────────┘
```

**Configuración:**
- Scorecard Clientes activos: fuente `v_executive_health`.
- Scorecards Nuevos / Recurrentes: fuente `v_monthly_metrics`, métricas `new_clients` y `recurring_clients`.
- Scorecard Churn 180d: fuente `v_executive_health`, campo `churn_rate_180d`.
- Scorecard AOV: fuente `v_executive_health`, campo `avg_order_value`.
- Barras horizontales de segmento RFM: fuente `v_rfm_segments`, dimensión `segment`, métrica `SUM(monetary)`. Activar "Mostrar porcentaje" para ver la participación de cada segmento en el revenue total. Champions = `#052DA6`, At Risk = `#D50E35`.
- Donut de clientes por segmento: fuente `v_rfm_segments`, dimensión `segment`, métrica `COUNT(client_id)`.
- Tabla At Risk: fuente `v_rfm_segments`, filtro `segment IN ("At Risk", "Hibernating")`. Activar botón de descarga (tres puntos → Exportar datos).

---

### Página 6 — Retention & Cohorts

```
┌──────────────────────────────────────────────────────────────────┐
│ Retention & Cohorts      [Fecha] [País] [Tipo cliente]           │
├──────────────────────┬───────────────────────┬───────────────────┤
│  Retención M1        │  % Champions          │  Churn 180d       │
│  promedio cohortes   │  en revenue           │                   │
├──────────────────────┴───────────────────────┴───────────────────┤
│ Heatmap de retención por cohorte                                  │
│ Fuente: v_cohort_retention                                        │
│ filas: cohort_month · columnas: months_since_first               │
│ valor: retention_pct · limitar columnas a 0–12                   │
│ escala: 0% = #D50E35 · 50% = #FDD315 · 100% = #4CAF7A           │
├──────────────────────────────────┬───────────────────────────────┤
│ Revenue mensual nuevo vs         │ % Revenue recurrente por mes  │
│ recurrente — barras apiladas     │ línea                         │
│ Fuente: v_monthly_metrics        │ Fuente: v_monthly_metrics     │
│ dimensión: month                 │ dimensión: month              │
│ métricas: new_client_revenue +   │ métrica: % Revenue Recurrente │
│ recurring_client_revenue         │ (campo calculado)             │
└──────────────────────────────────┴───────────────────────────────┘
```

**Configuración:**
- Scorecard Retención M1: fuente `v_cohort_retention`, filtro `months_since_first = 1`, métrica `AVG(retention_pct)`.
- Scorecard % Champions en revenue: fuente `v_executive_health`, campo `champions_revenue_pct`.
- Scorecard Churn 180d: fuente `v_executive_health`, campo `churn_rate_180d`.
- Heatmap de cohortes: usar Insertar → Tabla pivote. Filas = `cohort_month`, columnas = `months_since_first`, valor = `retention_pct` con escala de color. Limitar columnas a 0–12 para evitar cohortes con datos incompletos.
- Barras apiladas: fuente `v_monthly_metrics`. Serie 1 = `new_client_revenue` (acento secundario `#74ACDF`), serie 2 = `recurring_client_revenue` (acento principal `#052DA6`).
- Línea de % recurrente: fuente `v_monthly_metrics`, campo calculado `% Revenue Recurrente`. Dimensión `month`.

---

## 5. Filtros globales

Crear estos controles en cada página. Para replicarlos: copiar el control → pegar en otras páginas.

| Control | Tipo | Fuente | Campo | Aplica a |
|---|---|---|---|---|
| Rango de fechas | Date range control | `v_orders_enriched` | `registration_date` | Todas las páginas |
| País | Drop-down list | `v_orders_enriched` | `country` | Todas las páginas |
| Tipo de cliente | Drop-down list | `v_orders_enriched` | `client_type` | Todas las páginas |
| Categoría | Drop-down list | `v_order_lines` | `category` | Página 4 |

En páginas que combinan múltiples fuentes (p. ej., Página 3 usa `v_orders_enriched` y `v_country_clienttype_performance`), asegúrate de que cada control de filtro esté asociado a todas las fuentes presentes en esa página.

---

## 7. Trucos de Looker Studio

- **Tabla pivote para cohortes**: en lugar de una tabla normal, usa Insertar → Tabla pivote. Filas = `cohort_month`, columnas = `months_since_first`, valor = `retention_pct`. Agrega escala de color al valor.
- **Páginas ocultas**: crea páginas de detalle o anexos accesibles solo con link directo desde el menú de páginas.
- **Anotaciones en gráficos de línea**: usa "Agregar referencia" para marcar puntos de inflexión en la línea de revenue.
- **Mezcla de datos**: si necesitas cruzar `v_rfm_segments` con `v_orders_enriched` en una misma visual, usa el blending de Looker Studio en lugar de crear otra vista en BigQuery.
- **Filtros cruzados**: habilitar la interacción entre gráficos (clic en una barra filtra los demás) desde Recurso → Gestionar filtros → Habilitar filtrado cruzado.
- **Bookmarks por país o período**: duplica una página con filtros prefijados para presentaciones ejecutivas rápidas.


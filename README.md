> **Versión en español:** Saltar directamente a la sección en español buscando el encabezado **"— VERSIÓN EN ESPAÑOL —"**.

---

# TiendaLatam — Growth & Retention Analysis

End-to-end analysis of TiendaLatam's strategic pivot: a retail company that started with physical stores and has migrated its operations to a 100% digital model across 10 countries in Latin America. The project identifies growth levers, analyzes customer retention, and builds an executive dashboard in Looker Studio from raw data.

## The Business Problem

TiendaLatam is a retail company born as a brick-and-mortar chain that has completed its transition to a fully digital model across 10 Latin American countries (Argentina, Bolivia, Brazil, Chile, Colombia, Costa Rica, Ecuador, Mexico, Peru, and Uruguay). Its stores were converted into logistics distribution centers, eliminating the overhead of the physical model and passing those savings on to prices. By 2026, the executive team is formalizing this pivot with a strategy focused exclusively on competing online through price.

The key bets behind this pivot are:
- Competitive pricing as a non-negotiable promise.
- Converting the first order into a lasting relationship.
- Prioritizing markets where price sensitivity is highest.
- Reducing dependency on Technology.

The analysis aims to answer three key questions to build a data-driven roadmap:
1. Where does real growth come from, and where are we losing customers?
2. Which customer segments generate the most long-term value (LTV), and which are at risk of churning?
3. What product, pricing, and operational decisions can be made with the current data?

## Tech Stack

| Layer | Tool | Why |
|-------|------|-----|
| Storage + SQL | Google BigQuery | Serverless data warehouse, no setup required, standard SQL |
| Visualization | Looker Studio | Native BigQuery connector, shareable dashboards via public link |

See `ARCHITECTURE.md` for the complete data flow diagram.

## Repository Structure

```
proyecto-tiendalatam/
├── README.md                           # This file
├── ROADMAP.md                          # Execution plan
├── ARCHITECTURE.md                     # Data flow diagram
├── image.png                           # Looker Studio dashboard screenshot
├── data_expanded/                      # Dataset CSVs (11 tables, ~17k rows)
│   └── README.md                       # Description of each CSV file
├── sql/
│   ├── setup_views.sql                 # 9 analytical views for Looker Studio
│   ├── schema.sql                      # Postgres DDL (reference, not used in BQ)
│   ├── exploratory.sql                 # Initial dataset exploration
│   ├── growth_metrics.sql              # Growth KPIs
│   ├── growth_mom_by_country.sql       # MoM growth broken down by country
│   ├── growth_mom_colombia.sql         # Detailed Colombia analysis
│   ├── retention_rfm.sql               # Cohorts and RFM segmentation
│   ├── rfm_segmentation.sql            # Standalone RFM segmentation query
│   ├── rfm_segments_summary.sql        # RFM segment distribution summary
│   └── more_insights.sql               # Additional Product Management questions
└── docs/
    ├── setup_bigquery.md               # Step-by-step BigQuery setup guide
    ├── data_model.md                   # Data dictionary and relationships
    ├── business_questions.md           # The 15 questions answered by this project
    ├── business_mission_and_strategy.md# Mission, strategic context, and digital pivot
    ├── benchmark_tiendalatam_latam.md  # Competitive benchmark in LATAM
    ├── icp_analysis.md                 # Ideal Customer Profile (ICP) analysis
    ├── product_growth_metrics_ref.md   # Product growth metrics reference
    ├── findings_preliminary.md         # Findings executed against real data
    ├── early_notes.md                  # Initial exploratory notes
    └── dashboard_design.md             # Looker Studio dashboard structure
```

## Dataset

| Table | Rows | Description |
|-------|------|-------------|
| clients | 700 | Active and inactive customers, segmented by type |
| orders | 4,000 | Orders between July 2021 and April 2026 |
| order_details | 12,279 | Order line items with quantity and unit price |
| products | 50 | Product catalog across 8 categories |
| employees | 20 | Sales team distributed across 10 countries |
| locations | 10 | Logistics distribution points, one per LATAM country |
| categories | 8 | Technology, Home, Fashion, Beauty, Food, Sports, Toys, Stationery |
| client_types | 4 | Retailer, Wholesaler, Corporate, VIP |
| order_statuses | 6 | Pending, Processing, Shipped, Delivered, Cancelled, Returned |
| countries | 10 | LATAM countries |
| positions | 5 | Team roles |

# Key Findings — TiendaLatam Strategic Bets

[Dashboard access](https://datastudio.google.com/reporting/9dec01da-addc-4921-9df1-1bff8d7a887c)

---

## Bet 1 — Competitive Pricing as a Non-Negotiable Promise

### #1 · Delivery rate is 63.5% — 17 points below the regional benchmark

**Data:** 16.2% of orders blocked ≈ $316K in frozen GMV

Competitive pricing doesn't build a moat if 1 in 4 orders never arrives. The promise breaks at the most critical moment: delivery. A customer who pays and doesn't receive their order won't return, even if the price is the best in the market.

---

### #2 · 2 SKUs account for 46.2% of revenue — the Laptop is 30.8 days from a stockout

**Data:** Ultra-Light Laptop = 33.2% of total revenue

A stockout on the leading SKU is not an inventory problem — it's a direct threat to the pricing promise. If the product isn't available, the customer goes to a local retailer and the core business hypothesis is invalidated at that moment.

---

## Bet 2 — Converting the First Order into a Lasting Relationship

### #3 · The repurchase window is 74 days — after day 90, conversion drops sharply

**Data:** 61.2% made a second purchase — the remaining 38.8% is potentially lost

There is an expiration date for converting a buyer into a customer. Without an automated flow active on day 50, that customer silently churns and the acquisition cost goes unrecovered.

---

### #4 · 132 Champions generate 56.4% of revenue — with no active protection protocol in place

**Data:** More extreme concentration than the classic 80/20 rule

Losing 10 Champions hurts more than losing 100 new customers. This core group is the business's most valuable asset and also its greatest vulnerability — and today it has no documented active protection mechanism.

---

### #5 · Global churn at 23% — Retailers, the base segment, churn at 26.3%

**Data:** Benchmark for mature LATAM e-commerce: 15–20%

The segment that sustains the business (63.5% of revenue) is also the one abandoning most. The narrow spread across segments (23–26%) points to a systemic experience problem, not a specific segment with poor fit.

---

## Bet 3 — Prioritizing Markets Where Price Sensitivity Is Highest

### #6 · Colombia structurally underperforms despite having the same market maturity as Mexico

**Data:** Revenue/active month: Ecuador $3,372 vs. Colombia $2,084

Colombia has a triple problem — lower revenue, higher cancellation rate (6.69%), and lower AOV ($428) — that cannot be explained by market maturity alone. It is a combined operational and commercial diagnosis. Investing in acquisition before resolving this is wasting budget.

---

### #7 · Ecuador is the model the other 9 markets are not replicating

**Data:** Cancellation 3.75% · Delivery 66.6% · Revenue/month $3,372

The operational benchmark already exists within the business itself. If Ecuador can deliver better and cancel less under the same model, there is something in its local processes that is transferable — and that the other markets are not using today.

---

## Bet 4 — Reducing Dependency on Technology

### #8 · Home and Fashion have ~4,000 units sold but 3–6x less revenue than Technology

**Data:** Technology = 54.75% of revenue — target: reduce to 45%

Demand in these categories already exists — the gap is in average price per unit ($60 Home, $36 Fashion). Diversification doesn't require generating new demand; it requires raising the ticket in categories where customers are already buying.

---

### #9 · LTV spread across the 4 segments is just 17% — VIP has lower LTV than Retailer

**Data:** Corporate $2,425 · Retailer $2,387 · VIP $2,347 · Wholesaler $1,999

If segments don't behave differently in value, they aren't real segments — they're labels. This makes it impossible to design differentiated value propositions by customer type, which is exactly what catalog diversification needs to work: knowing who buys what and at what price.

## About the Author

Diana Mildred Galindo | Product Manager and User Experience Expert | [LinkedIn](https://www.linkedin.com/in/diana-mildred/) | [Website](https://dianamildred.lovable.app/)

"TiendaLatam is a hypothetical case study I built because I genuinely love diving deep into problems, understanding them thoroughly, and finding solutions."

## How to Replicate It

Follow my roadmap, which will take you from raw data to a product roadmap ready to execute. See `ROADMAP.md`.

---
---

# — VERSIÓN EN ESPAÑOL —

---

# TiendaLatam — Análisis de Growth & Retención

Análisis end-to-end del pivote estratégico de TiendaLatam: una empresa de retail que comenzó con tiendas presenciales y ha migrado su operación a un modelo 100% digital en 10 países de Latinoamérica. El proyecto identifica palancas de crecimiento, analiza la retención de clientes y construye un dashboard ejecutivo en Looker Studio a partir de los datos crudos.

## El problema de negocio

TiendaLatam es una empresa de retail que nació como cadena de tiendas presenciales y ha completado su transición a un modelo 100% digital en 10 países de Latinoamérica (Argentina, Bolivia, Brasil, Chile, Colombia, Costa Rica, Ecuador, México, Perú y Uruguay). Sus tiendas se reconvirtieron en centros de distribución logística, eliminando el costo del modelo presencial para trasladarlo al precio. Para 2026, el equipo directivo está formalizando este pivote con una estrategia orientada a competir exclusivamente por precio en línea.

Las apuestas del negocio para este pivote son:
- Precio competitivo como promesa no negociable.
- Convertir el primer pedido en una relación duradera.
- Priorizar mercados donde el precio duele más.
- Reducir la dependencia de Tecnología.

El análisis busca responder tres preguntas clave para construir un roadmap basado en datos:

1. ¿De dónde viene el crecimiento real y dónde estamos perdiendo clientes?
2. ¿Qué segmentos de clientes generan más valor a largo plazo (LTV) y cuáles están en riesgo de churn?
3. ¿Qué decisiones de producto, pricing y operación pueden tomarse con los datos actuales?

## Stack técnico

| Capa | Herramienta | Por qué |
|------|------------|---------|
| Almacenamiento + SQL | Google BigQuery | Data warehouse serverless, sin instalación, SQL estándar |
| Visualización | Looker Studio | Conector nativo a BigQuery, dashboards compartibles vía link público |

Ver `ARCHITECTURE.md` para el diagrama completo del flujo de datos.

## Estructura del repositorio

```
proyecto-tiendalatam/
├── README.md                           # Este archivo
├── ROADMAP.md                          # Plan de ejecución de 5 días
├── ARCHITECTURE.md                     # Diagrama del flujo de datos
├── image.png                           # Captura del dashboard en Looker Studio
├── data_expanded/                      # CSVs del dataset (11 tablas, ~17k filas)
│   └── README.md                       # Descripción de cada archivo CSV
├── sql/
│   ├── setup_views.sql                 # 9 vistas analíticas para Looker Studio
│   ├── schema.sql                      # DDL Postgres (referencia, no usado en BQ)
│   ├── exploratory.sql                 # Exploración inicial del dataset
│   ├── growth_metrics.sql              # KPIs de crecimiento
│   ├── growth_mom_by_country.sql       # Crecimiento MoM desglosado por país
│   ├── growth_mom_colombia.sql         # Análisis detallado Colombia
│   ├── retention_rfm.sql               # Cohortes y segmentación RFM
│   ├── rfm_segmentation.sql            # Query de segmentación RFM standalone
│   ├── rfm_segments_summary.sql        # Resumen de distribución por segmento RFM
│   └── more_insights.sql               # Preguntas adicionales de Product Management
└── docs/
    ├── setup_bigquery.md               # Guía paso a paso de setup en BigQuery
    ├── data_model.md                   # Diccionario de datos y relaciones
    ├── business_questions.md           # Las 15 preguntas que responde el proyecto
    ├── business_mission_and_strategy.md# Misión, contexto estratégico y pivote digital
    ├── benchmark_tiendalatam_latam.md  # Benchmark competitivo en LATAM
    ├── icp_analysis.md                 # Análisis del perfil de cliente ideal (ICP)
    ├── product_growth_metrics_ref.md   # Referencia de métricas de product growth
    ├── findings_preliminary.md         # Hallazgos ejecutados contra los datos reales
    ├── early_notes.md                  # Notas exploratorias iniciales
    └── dashboard_design.md             # Estructura del dashboard en Looker Studio
```

## Dataset

| Tabla | Filas | Descripción |
|-------|-------|-------------|
| clients | 700 | Clientes activos e inactivos, segmentados por tipo |
| orders | 4,000 | Pedidos entre julio 2021 y abril 2026 |
| order_details | 12,279 | Líneas de pedido con cantidad y precio unitario |
| products | 50 | Catálogo de productos en 8 categorías |
| employees | 20 | Equipo de ventas distribuido en 10 países |
| locations | 10 | Puntos de distribución logística, uno por país LATAM |
| categories | 8 | Tecnología, Hogar, Moda, Belleza, Alimentos, Deportes, Juguetería, Papelería |
| client_types | 4 | Minorista, Mayorista, Corporativo, VIP |
| order_statuses | 6 | Pendiente, Procesando, Enviado, Entregado, Cancelado, Devuelto |
| countries | 10 | Países LATAM |
| positions | 5 | Cargos del equipo |

# Principales Hallazgos — Apuestas Estratégicas TiendaLatam

[Dashboard access](https://datastudio.google.com/reporting/9dec01da-addc-4921-9df1-1bff8d7a887c)
---

## Apuesta 1 — Precio competitivo como promesa no negociable

### #1 · La tasa de entrega es del 63.5% — 17 puntos por debajo del benchmark regional

**Dato:** 16.2% de órdenes bloqueadas ≈ $316K de GMV congelado

El precio competitivo no genera moat si 1 de cada 4 órdenes no llega. La promesa se rompe en el momento más importante: la entrega. Un cliente que paga y no recibe su pedido no vuelve, aunque el precio sea el mejor del mercado.

---

### #2 · 2 SKUs concentran el 46.2% del revenue — la Laptop está a 30.8 días de quiebre de stock

**Dato:** Laptop Ultraliviana = 33.2% del revenue total

Un quiebre de stock en el SKU líder no es un problema de inventario: es una amenaza directa a la promesa de precio. Si el producto no está disponible, el cliente va al comercio local y la hipótesis central del negocio se invalida en ese momento.

---

## Apuesta 2 — Convertir el primer pedido en una relación duradera

### #3 · La ventana de recompra es de 74 días — después del día 90 la conversión cae abruptamente

**Dato:** 61.2% realizó una segunda compra — el 38.8% restante está potencialmente perdido

Hay una fecha de caducidad para convertir un comprador en cliente. Sin un flujo automático activo en el día 50, ese cliente abandona silenciosamente y el costo de adquisición queda sin recuperar.

---

### #4 · 132 Champions generan el 56.4% del revenue — sin protocolo de protección activo

**Dato:** Concentración más extrema que la regla 80/20 clásica

Perder 10 Champions duele más que perder 100 clientes nuevos. Este núcleo es el activo más valioso del negocio y también su mayor fragilidad — y hoy no tiene ningún mecanismo activo de protección documentado.

---

### #5 · Churn global del 23% — los Minoristas, el segmento base, churnan al 26.3%

**Dato:** Benchmark e-commerce LATAM maduro: 15–20%

El segmento que sostiene el negocio (63.5% del revenue) es también el que más abandona. El spread mínimo entre segmentos (23–26%) apunta a un problema sistémico de experiencia, no a un segmento puntual con mal fit.

---

## Apuesta 3 — Priorizar mercados donde el precio duele más

### #6 · Colombia tiene un underperformance estructural pese a tener la misma madurez de mercado que México

**Dato:** Revenue/mes activo: Ecuador $3,372 vs. Colombia $2,084

Colombia tiene un triple problema — menor revenue, mayor tasa de cancelación (6.69%) y menor AOV ($428) — que no se explica por la madurez del mercado. Es un diagnóstico combinado operativo-comercial. Invertir en adquisición antes de resolver esto es desperdiciar el presupuesto.

---

### #7 · Ecuador es el modelo que los otros 9 mercados no están replicando

**Dato:** Cancelación 3.75% · Entrega 66.6% · Revenue/mes $3,372

El benchmark operativo existe dentro del propio negocio. Si Ecuador logra entregar mejor y cancelar menos con el mismo modelo, hay algo en sus procesos locales que es transferible — y que los demás mercados no están usando hoy.

---

## Apuesta 4 — Reducir dependencia de Tecnología

### #8 · Hogar y Moda tienen ~4,000 unidades vendidas pero generan 3–6 veces menos revenue que Tecnología

**Dato:** Tecnología = 54.75% del revenue — objetivo: reducir al 45%

La demanda en estas categorías ya existe; la brecha está en el precio promedio por unidad ($60 Hogar, $36 Moda). Diversificar no requiere generar nueva demanda: requiere elevar el ticket en categorías donde los clientes ya están comprando.

---

### #9 · El spread de LTV entre los 4 segmentos es de apenas el 17% — VIP tiene menor LTV que Minorista

**Dato:** Corporativo $2,425 · Minorista $2,387 · VIP $2,347 · Mayorista $1,999

Si los segmentos no se comportan de forma diferente en valor, no son segmentos reales: son etiquetas. Esto impide diseñar propuestas de valor diferenciadas por tipo de cliente, que es exactamente lo que necesita la diversificación del catálogo para funcionar: saber quién compra qué y a qué precio.

## Sobre la autora

Diana Mildred Galindo | Product Manager and User experience expert | [LinkedIn](https://www.linkedin.com/in/diana-mildred/) | [Website](https://dianamildred.lovable.app/)

"TiendaLatam es un caso de estudio hipotético que construí porque, genuinamente, me encanta envolverme en problemas, conocerlos profundamente y buscarles soluciones."

## Cómo replicarlo

Sigue mi roadmap, que te llevará desde la data cruda hasta un roadmap de producto listo para ejecutar. Ver `ROADMAP.md`.

# TiendaLatam — Análisis de Growth & Retención

Análisis end-to-end del pivote estratégico de TiendaLatam: una empresa de retail que comenzó con tiendas presenciales y ha migrado su operación a un modelo 100% digital en 10 países de Latinoamérica. El proyecto identifica palancas de crecimiento, analiza retención de clientes y construye un dashboard ejecutivo en Looker Studio desde los datos crudos. 

## El problema de negocio

TiendaLatam es una empresa de retail que nació como cadena de tiendas presenciales y ha completado su transición a un modelo 100% digital en 10 países de Latinoamérica (Argentina, Bolivia, Brasil, Chile, Colombia, Costa Rica, Ecuador, México, Perú y Uruguay). Sus tiendas se reconvirtieron en centros de distribución logística, eliminando el costo del modelo presencial para trasladarlo al precio. Para el 2026, el equipo directivo está formalizando este pivote con una estrategia orientada a competir exclusivamente por precio online.

Las apuestas del negocio para este pivot son:
- Precio competitivo como promesa no negociable.
- Convertir el primer pedido en una relación duradera.
- Priorizar mercados donde el precio duele más.
- Reducir dependencia de Tecnología.

 El análisis busca responder tres preguntas clave para construir un roadmap basado en datos:

1. ¿De dónde viene el crecimiento real y dónde estamos perdiendo clientes?
2. ¿Qué segmentos de clientes generan más valor a largo plazo (LTV) y cuáles están en riesgo de churn?
3. ¿Qué decisiones de producto, pricing y operación pueden tomarse con los datos actuales?

## Stack técnico

| Capa | Herramienta | Por qué |
|------|------------|---------|
| Almacenamiento + SQL | Google BigQuery | Data warehouse serverless, sin instalación, SQL estándar |
| Visualización | Looker Studio | Conector nativo a BigQuery, dashboards compartibles vía link público |

Ver `ARCHITECTURE.md` para el diagrama completo del flujo de datos.

## Estructura del repositorio

```
proyecto-tiendalatam/
├── README.md                           # Este archivo
├── ROADMAP.md                          # Plan de ejecución
├── ARCHITECTURE.md                     # Diagrama del flujo de datos
├── image.png                           # Captura del dashboard en Looker Studio
├── data_expanded/                      # CSVs del dataset (11 tablas, ~17k filas)
│   └── README.md                       # Descripción de cada archivo CSV
├── sql/
│   ├── setup_views.sql                 # 9 vistas analíticas para Looker Studio
│   ├── schema.sql                      # DDL Postgres (referencia, no usado en BQ)
│   ├── exploratory.sql                 # Exploración inicial del dataset
│   ├── growth_metrics.sql              # KPIs de crecimiento
│   ├── growth_mom_by_country.sql       # Crecimiento MoM desglosado por país
│   ├── growth_mom_colombia.sql         # Análisis detallado Colombia
│   ├── retention_rfm.sql               # Cohortes y segmentación RFM
│   ├── rfm_segmentation.sql            # Query de segmentación RFM standalone
│   ├── rfm_segments_summary.sql        # Resumen de distribución por segmento RFM
│   └── more_insights.sql               # Preguntas adicionales de Product Management
└── docs/
    ├── setup_bigquery.md               # Guía paso a paso de setup en BigQuery
    ├── data_model.md                   # Diccionario de datos y relaciones
    ├── business_questions.md           # Las 15 preguntas que responde el proyecto
    ├── business_mission_and_strategy.md# Misión, contexto estratégico y pivote digital
    ├── benchmark_tiendalatam_latam.md  # Benchmark competitivo en LATAM
    ├── icp_analysis.md                 # Análisis del perfil de cliente ideal (ICP)
    ├── product_growth_metrics_ref.md   # Referencia de métricas de product growth
    ├── findings_preliminary.md         # Hallazgos ejecutados contra los datos reales
    ├── early_notes.md                  # Notas exploratorias iniciales
    └── dashboard_design.md             # Estructura del dashboard en Looker Studio
```

## Dataset

| Tabla | Filas | Descripción |
|-------|-------|-------------|
| clients | 700 | Clientes activos e inactivos, segmentados por tipo |
| orders | 4,000 | Pedidos entre julio 2021 y abril 2026 |
| order_details | 12,279 | Líneas de pedido con cantidad y precio unitario |
| products | 50 | Catálogo de productos en 8 categorías |
| employees | 20 | Equipo de ventas distribuido en 10 países |
| locations | 10 | Puntos de distribución logística, uno por país LATAM |
| categories | 8 | Tecnología, Hogar, Moda, Belleza, Alimentos, Deportes, Juguetería, Papelería |
| client_types | 4 | Minorista, Mayorista, Corporativo, VIP |
| order_statuses | 6 | Pendiente, Procesando, Enviado, Entregado, Cancelado, Devuelto |
| countries | 10 | Países LATAM |
| positions | 5 | Cargos del equipo |

# Principales Hallazgos — Apuestas Estratégicas TiendaLatam

---

## Apuesta 1 — Precio competitivo como promesa no negociable

### #1 · La tasa de entrega es del 63.5% — 17 puntos por debajo del benchmark regional

**Dato:** 16.2% de órdenes bloqueadas ≈ $316K de GMV congelado

El precio competitivo no genera moat si 1 de cada 4 órdenes no llega. La promesa no se cumple en el momento más importante: la entrega. Un cliente que paga y no recibe no vuelve aunque el precio sea el mejor del mercado.

---

### #2 · 2 SKUs concentran el 46.2% del revenue — la Laptop está a 30.8 días de quiebre de stock

**Dato:** Laptop Ultraliviana = 33.2% del revenue total

Un quiebre de stock en el SKU líder no es un problema de inventario — es una amenaza directa a la promesa de precio. Si el producto no está disponible, el cliente va al comercio local y la hipótesis central del negocio se invalida en ese momento.

---

## Apuesta 2 — Convertir el primer pedido en una relación duradera

### #3 · La ventana de recompra es de 74 días — después del día 90 la conversión cae abruptamente

**Dato:** 61.2% hizo una segunda compra — el 38.8% restante está potencialmente perdido

Hay una fecha de caducidad para convertir un comprador en cliente. Sin un flujo automático activo en el día 50, ese cliente abandona silenciosamente y el costo de adquisición queda sin recuperar.

---

### #4 · 132 Champions generan el 56.4% del revenue — sin protocolo de protección activo

**Dato:** Concentración más extrema que la regla 80/20 clásica

Perder 10 Champions duele más que perder 100 clientes nuevos. Este núcleo es el activo más valioso del negocio y también su mayor fragilidad — y hoy no tiene ningún mecanismo activo de protección documentado.

---

### #5 · Churn global del 23% — los Minoristas, el segmento base, churnan al 26.3%

**Dato:** Benchmark e-commerce LATAM maduro: 15–20%

El segmento que sostiene el negocio (63.5% del revenue) es también el que más abandona. El spread mínimo entre segmentos (23–26%) apunta a un problema sistémico de experiencia, no a un segmento puntual con mal fit.

---

## Apuesta 3 — Priorizar mercados donde el precio duele más

### #6 · Colombia underperforma estructuralmente pese a tener el mismo tiempo de vida que México

**Dato:** Revenue/mes activo: Ecuador $3,372 vs Colombia $2,084

Colombia tiene un triple problema — menor revenue, mayor cancelación (6.69%) y menor AOV ($428) — que no se explica por madurez del mercado. Es un diagnóstico combinado operativo-comercial. Invertir en adquisición antes de resolver esto es desperdiciar el presupuesto.

---

### #7 · Ecuador es el modelo que los otros 9 mercados no están replicando

**Dato:** Cancelación 3.75% · Entrega 66.6% · Revenue/mes $3,372

El benchmark operativo existe dentro del propio negocio. Si Ecuador logra entregar mejor y cancelar menos con el mismo modelo, hay algo en sus procesos locales que es transferible — y que los demás mercados no están usando hoy.

---

## Apuesta 4 — Reducir dependencia de Tecnología

### #8 · Hogar y Moda tienen ~4,000 unidades vendidas pero 3–6x menos revenue que Tecnología

**Dato:** Tecnología = 54.75% del revenue — objetivo: reducir a 45%

La demanda en estas categorías ya existe — el gap es de precio promedio por unidad ($60 Hogar, $36 Moda). Diversificar no requiere generar nueva demanda; requiere elevar el ticket en categorías donde los clientes ya están comprando.

---

### #9 · El LTV spread entre los 4 segmentos es de apenas el 17% — VIP tiene menor LTV que Minorista

**Dato:** Corporativo $2,425 · Minorista $2,387 · VIP $2,347 · Mayorista $1,999

Si los segmentos no se comportan distinto en valor, no son segmentos reales — son etiquetas. Esto impide diseñar propuestas de valor diferenciadas por tipo de cliente, que es exactamente lo que necesita la diversificación de catálogo para funcionar: saber quién compra qué y por cuánto.

## Sobre la autora

Diana Mildred Galindo | Product Manager and User experience expert | [LinkedIn](https://www.linkedin.com/in/diana-mildred/) | [Website](https://dianamildred.lovable.app/)

"TiendaLatam es un caso de estudio hipotético que construí porque, genuinamente, me encanta envolverme en problemas, conocerlos profundamente y buscarles soluciones."

## Cómo replicarlo

Sigue mi roadmap te llevara desde la data cruda, hasta un roadmap de producto listo ejecutar. `ROADMAP.md`
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
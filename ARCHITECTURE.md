> **Versión en español:** Saltar directamente a la sección en español buscando el encabezado **"— VERSIÓN EN ESPAÑOL —"**.

---

# Architecture

This document explains how the project is organized technically: what each tool does, why it was chosen, and how information flows from the raw CSVs to the dashboard published on your website. It is designed to help you develop a deep understanding of the architecture — and to serve as a practical exercise in architectural thinking for PMs.

## Overview (in one sentence)

The original CSVs are loaded into BigQuery (a cloud data warehouse), where all analysis is performed in SQL; the results are connected to Looker Studio (a BI tool), which generates an interactive dashboard accessible via a public link that can be embedded in your website.

## Architecture Diagram

```
┌─────────────────┐
│  11 original    │
│  CSV files      │   (Project data)
│  (data_expanded/)│
└────────┬────────┘
         │
         │  one-time manual load via BigQuery UI
         │  (drag & drop, schema auto-detection)
         ▼
┌──────────────────────────────────────────────────┐
│           Google BigQuery (Sandbox)              │
│  ─────────────────────────────────────────────  │
│  Project: tiendalatam-casestudy                  │
│  Dataset: tiendalatam                            │
│                                                  │
│  Base tables (11):                               │
│    clients, orders, order_details, products,     │
│    employees, locations, categories,             │
│    countries, client_types, order_statuses,      │
│    positions                                     │
│                                                  │
│  Analytical views (created with setup_views.sql):│
│    v_orders_enriched          (orders + joins)   │
│    v_monthly_metrics          (monthly revenue)  │
│    v_executive_health         (KPI scorecards)   │
│    v_country_clienttype_performance (by country) │
│    v_rfm_segments             (RFM segments)     │
│    v_cohort_retention         (cohorts)          │
│    v_abc_classification       (ABC classification│
│    v_stock_alerts             (stock alerts)     │
│    v_order_lines              (order line items) │
│                                                  │
│  Cost: $0 (sandbox, no credit card required)     │
└────────────────────────┬─────────────────────────┘
                         │
                         │  native BigQuery connector
                         │  (authentication via your Google account)
                         ▼
┌──────────────────────────────────────────────────┐
│            Looker Studio (BI tool)               │
│  ─────────────────────────────────────────────  │
│  Report: TiendaLatam – Growth & Retention        │
│                                                  │
│  Pages:                                          │
│    1. Overview                                   │
│    2. Revenue & Finance                          │
│    3. Orders & Operations                        │
│    4. Products & Catalog                         │
│    5. Customers                                  │
│    6. Retention & Cohorts                        │
│                                                  │
│  Cost: $0 (always free)                          │
└────────────────────────┬─────────────────────────┘
                         │
                         │  public link + iframe embed
                         ▼
┌──────────────────────────────────────────────────┐
│              Your personal website               │
│  ─────────────────────────────────────────────  │
│  Case study: TiendaLatam                         │
│    • Problem context                             │
│    • Key findings (3–5 insights)                 │
│    • Embedded dashboard (live)                   │
│    • Product recommendations                     │
└──────────────────────────────────────────────────┘
```

## The 3 Architecture Layers

### Layer 1 — Storage & Processing (BigQuery)

BigQuery is Google's serverless data warehouse. "Serverless" means you don't manage any servers or installations: you upload data, write SQL, and Google handles the rest.

**What it does in this project:**
- Stores the 11 original tables.
- Runs all SQL queries in the analysis (the files in the `sql/` directory).
- Materializes 9 analytical views (pre-computed queries) so Looker Studio doesn't have to recompute them on every load.

**Why BigQuery and not something else:**
- 100% free Sandbox, no credit card required.
- SQL syntax very close to PostgreSQL.
- Native connector to Looker Studio: one click.
- The most widely used data warehouse in startups and tech companies across LATAM — putting your name close to that ecosystem.

**What it costs:**
- Storage: free up to 10 GB. This project weighs less than 1 MB.
- Queries: free up to 1 TB processed per month. Each query in this project processes kilobytes.
- Limitation: tables in Sandbox expire after 60 days. Easy fix: reload them (10 min) or activate the free GCP trial (90 days + $300 USD in credits, does not auto-charge when it ends).

### Layer 2 — Visualization & Exploration (Looker Studio)

Looker Studio (formerly Google Data Studio) is Google's free BI tool. It lets you drag and drop fields to build visuals connected to data sources.

**What it does in this project:**
- Reads the BigQuery views.
- Renders 6 pages of interactive dashboard.
- Applies global filters (country, date, client type).
- Publishes the dashboard via a public link.

**Why Looker Studio and not Power BI / Tableau:**
- 100% web-based — no installation required, works on your Mac.
- Free with no locked features.
- Generates shareable public links (Power BI Free does not allow this).
- Native integration with BigQuery: zero connection configuration.

**Honest limitations:**
- Some advanced visuals (a perfect cohort heatmap, scatter plots with rich tooltips) are less polished than in Tableau.
- Complex calculations in Looker Studio use "calculated fields" (formula-like syntax), not DAX. The strategy here is to keep heavy calculations in SQL (BigQuery) and let Looker Studio handle visualization only.

---
---

# — VERSIÓN EN ESPAÑOL —

---

# Arquitectura

Este documento explica cómo está organizado el proyecto técnicamente: qué herramienta hace qué, por qué fue elegida y cómo fluye la información desde los CSVs hasta el dashboard publicado en tu sitio web. Está pensado para que desarrolles una comprensión profunda de la arquitectura, y para que sirva como ejercicio práctico de pensamiento arquitectónico para PMs.

## Vista panorámica (en una frase)

Los CSVs originales se cargan en BigQuery (data warehouse en la nube), donde todo el análisis se realiza en SQL; los resultados se conectan a Looker Studio (herramienta de BI), que genera un dashboard interactivo accesible mediante un link público que puede incrustarse en tu sitio web.

## Diagrama de la arquitectura

```
┌─────────────────┐
│  11 archivos    │
│  CSV originales │   (Data del proyecto)
│  (data_expanded/)│
└────────┬────────┘
         │
         │  carga manual una sola vez vía UI de BigQuery
         │  (drag & drop, autodetección de esquema)
         ▼
┌──────────────────────────────────────────────────┐
│           Google BigQuery (Sandbox)              │
│  ─────────────────────────────────────────────  │
│  Proyecto: tiendalatam-casestudy                 │
│  Dataset:  tiendalatam                           │
│                                                  │
│  Tablas base (11):                               │
│    clients, orders, order_details, products,     │
│    employees, locations, categories,             │
│    countries, client_types, order_statuses,      │
│    positions                                     │
│                                                  │
│  Vistas analíticas (creadas con setup_views.sql):│
│    v_orders_enriched          (orders + joins)   │
│    v_monthly_metrics          (revenue mensual)  │
│    v_executive_health         (scorecards KPI)   │
│    v_country_clienttype_performance (por país)   │
│    v_rfm_segments             (segmentos RFM)    │
│    v_cohort_retention         (cohortes)         │
│    v_abc_classification       (clasificación ABC)│
│    v_stock_alerts             (alertas de stock) │
│    v_order_lines              (líneas de pedido) │
│                                                  │
│  Costo: $0 (sandbox sin tarjeta de crédito)      │
└────────────────────────┬─────────────────────────┘
                         │
                         │  conector nativo BigQuery
                         │  (autenticación con tu cuenta de Google)
                         ▼
┌──────────────────────────────────────────────────┐
│            Looker Studio (herramienta BI)        │
│  ─────────────────────────────────────────────  │
│  Informe: TiendaLatam – Growth & Retention       │
│                                                  │
│  Páginas:                                        │
│    1. Resumen ejecutivo                          │
│    2. Revenue y finanzas                         │
│    3. Órdenes y operaciones                      │
│    4. Productos y catálogo                       │
│    5. Clientes                                   │
│    6. Retención y cohortes                       │
│                                                  │
│  Costo: $0 (gratuito siempre)                    │
└────────────────────────┬─────────────────────────┘
                         │
                         │  link público + iframe embed
                         ▼
┌──────────────────────────────────────────────────┐
│              Tu sitio web personal               │
│  ─────────────────────────────────────────────  │
│  Caso de estudio: TiendaLatam                    │
│    • Contexto del problema                       │
│    • Hallazgos clave (3–5 insights)              │
│    • Dashboard incrustado (en vivo)              │
│    • Recomendaciones de producto                 │
└──────────────────────────────────────────────────┘
```

## Las 3 capas de la arquitectura

### Capa 1 — Almacenamiento y procesamiento (BigQuery)

BigQuery es el data warehouse serverless de Google. "Serverless" significa que no gestionas servidores ni instalaciones: subes los datos, escribes SQL y Google se encarga del resto.

**Qué hace en este proyecto:**
- Almacena las 11 tablas originales.
- Ejecuta todas las consultas SQL del análisis (los archivos en el directorio `sql/`).
- Materializa 9 vistas analíticas (queries pre-calculados) para que Looker Studio no tenga que recomputarlos en cada carga.

**Por qué BigQuery y no otra herramienta:**
- Sandbox 100% gratuito, sin tarjeta de crédito.
- Sintaxis SQL muy cercana a PostgreSQL.
- Conector nativo a Looker Studio: un solo clic.
- Es el data warehouse más utilizado en startups y empresas tech en LATAM, lo que acerca tu perfil a ese ecosistema.

**Lo que cuesta:**
- Almacenamiento: gratuito hasta 10 GB. Este proyecto pesa menos de 1 MB.
- Consultas: gratuitas hasta 1 TB procesado por mes. Cada consulta en este proyecto procesa kilobytes.
- Limitación: las tablas en Sandbox expiran a los 60 días. Solución sencilla: recargarlas (10 minutos) o activar la prueba gratuita de GCP (90 días + USD $300 en créditos, no cobra automáticamente al terminar).

### Capa 2 — Visualización y exploración (Looker Studio)

Looker Studio (antes Google Data Studio) es la herramienta de BI gratuita de Google. Permite arrastrar campos y construir visualizaciones conectadas a fuentes de datos.

**Qué hace en este proyecto:**
- Lee las vistas de BigQuery.
- Renderiza 6 páginas de dashboard interactivo.
- Aplica filtros globales (país, fecha, tipo de cliente).
- Publica el dashboard mediante un link público.

**Por qué Looker Studio y no Power BI o Tableau:**
- 100% web: no requiere instalación y funciona en cualquier sistema operativo.
- Gratuito sin funcionalidades bloqueadas.
- Genera links públicos compartibles (Power BI Free no lo permite).
- Integración nativa con BigQuery: cero configuración de conexión.

**Limitaciones honestas:**
- Algunos visuales avanzados (un cohort heatmap perfecto, scatter plots con tooltips enriquecidos) son menos pulidos que en Tableau.
- Los cálculos complejos en Looker Studio se realizan con "campos calculados" (sintaxis tipo fórmula), no con DAX. La estrategia aquí es dejar los cálculos pesados en SQL (BigQuery) y que Looker Studio se encargue únicamente de la visualización.
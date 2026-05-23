> **Versión en español:** Saltar directamente a la sección en español buscando el encabezado **"— VERSIÓN EN ESPAÑOL —"**.

---

# Roadmap — TiendaLatam Growth & Retention Analysis

This roadmap walks you through the process I followed for this analysis: from the technical setup, through the data analysis, to the final result. It gives you a clear view of my process and allows you to replicate it if you choose. I am happy to answer any questions or receive feedback at any time, feel free to reach out at: dianamildred.dsgn@gmail.com.

---

## Phase 1 — Setup & Exploration (Foundation)

**Objective:** Set up BigQuery, load the data, run the first exploration, and establish business context.

Tasks:
- Create a Google Cloud account (free, no credit card required) and a project called `tiendalatam-casestudy`. Follow `docs/setup_bigquery.md` step by step.
- Enable BigQuery Sandbox and create the `tiendalatam` dataset.
- Load the CSVs from `data_expanded/` using schema auto-detection.
- Use AI to generate an EDA plan and execute it. `sql/exploratory.sql` contains 6 queries that provide a general overview: volume, dates, status distribution, and top products.
- Use AI to create a `product_growth_metrics_ref` document mapping the ideal metrics universe by product type, and evaluate what can be built from the existing dataset.
- Document business considerations around how metrics are calculated. For example, some companies calculate revenue using only orders with `delivered` status, while others also include `shipped`. Clarify each metric and document the relevant nuances so they are accounted for during AI-assisted processing. `CLAUDE`
- Use AI to generate `findings_preliminary`: analyze findings, document initial observations, and capture the questions that arise (`early_notes`).
- Conduct discovery sessions on the points most relevant to your goal. A couple of sessions with someone who has deep domain knowledge will significantly improve the quality of your insights.

> **Tip:** Take your time with this phase. Feeling lost here is normal, it's a lot of information for a human brain, but not for AI. Lean on it to resolve questions, generate queries quickly, or request pre-processed data. Everything starts to make sense as you spend more time with the data and build context.

---

## Phase 2 — Data Strategy: Defining Business Questions

**Objective:** Define the questions the business needs to answer, aligned with the company's mission and strategy. Then build and run the queries that answer them.

Tasks:
- Review the company's mission and strategy to align any data structuring and insight generation with the direction the business is pursuing. In this case, I built a hypothetical mission and strategy.
- Using `early_notes` as input, build a list of questions aligned with the product type and company strategy (`business_questions`). Use AI to surface questions you hadn't considered.
- Identify the relevant business metrics for the product's industry. Use AI to validate which ones can be built from the existing dataset (`reference_metrics.md`).
- Build the queries that will answer each of the `business_questions` based on the dataset.
- Answer all business questions using the queries built, and document the findings, follow-up questions, and data gaps identified (`business_questions.md`).

---

## Phase 3 — Dashboard in Data Studio

**Objective:** Materialize the findings in an executive dashboard published in the cloud.

Tasks:
- Based on the queries built, use AI to generate calculated BigQuery views that will simplify the connection with Data Studio.
- Open Data Studio (lookerstudio.google.com) with the same Google account.
- Connect the following BigQuery views as data sources: `v_orders_enriched`, `v_order_lines`, `v_rfm_segments`, `v_cohort_retention`, `v_monthly_metrics`, `stock_alerts`, `executive_health`, `customer_funnel`, `abc_classification`, `country_performance`, `country_clienttype_performance`.
- Define the dashboard structure in draft form to identify the chart type that best represents each piece of information:
  1. **Resumen ejecutivo** — KPIs principales (revenue, órdenes, AOV, clientes activos), tendencia mensual y mapa de revenue por país.
  2. **Órdenes y operaciones** — Total de órdenes, órdenes válidas, órdenes de los últimos 180 días, % entregadas, % en progreso, % con problemas, % canceladas, % devueltas. Rendimiento operativo por país, distribución de cancelaciones por país, órdenes mensuales por país.
  3. **Productos y catálogo** — Categorías principales, treemap por producto, análisis ABC, alertas de stock.
  4. **Crecimiento** — Crecimiento MoM, clientes nuevos vs. recurrentes, retención mes 1.
  5. **Retención y cohortes** — Revenue, AOV, tasa de churn, retención por cohorte, revenue recurrente vs. nuevos clientes, revenue por país, AOV por tipo de cliente.
  6. **Clientes** — Distribución de segmentos, heatmap de cohortes, lista de clientes en riesgo, distribución por tipo de usuario.
- Construir las páginas del dashboard siguiendo la estructura definida. Ver `docs/dashboard_design.md`.

---

## Phase 4 — Roadmap

**Objective:** Synthesize the findings and build a prioritized action roadmap.

Tasks:
- Propose actionable initiatives for the company based on the findings.
- Prioritize the initiatives according to the company's strategy using the ICE framework. (`business_roadmap.md`)

---
---

# — VERSIÓN EN ESPAÑOL —

---

# Roadmap — TiendaLatam Growth & Retention Analysis

Este roadmap te lleva, paso a paso, por el proceso que seguí para este análisis: desde la construcción técnica, pasando por el análisis de datos, hasta el resultado final. Te dará una visión clara del proceso que realicé y te permitirá replicarlo si así lo deseas. Estoy disponible para responder cualquier pregunta o recibir feedback en cualquier momento; puedes contactarme en: dianamildred.dsgn@gmail.com.

---

## Fase 1 — Setup y exploración (Foundation)

**Objetivo:** Montar BigQuery, cargar los datos, realizar la primera exploración y establecer el contexto de negocio.

Tareas:
- Crear una cuenta de Google Cloud (gratuita, sin tarjeta de crédito) y un proyecto llamado `tiendalatam-casestudy`. Seguir `docs/setup_bigquery.md` paso a paso.
- Activar BigQuery Sandbox y crear el dataset `tiendalatam`.
- Cargar los CSVs de `data_expanded/` con autodetección de esquema.
- Generar con IA un plan de EDA y ejecutarlo. `sql/exploratory.sql` contiene 6 queries que dan el panorama general: volumen, fechas, distribución de estados y productos principales.
- Usar IA para crear un documento `product_growth_metrics_ref` que mapee el universo ideal de métricas según el tipo de producto, y evaluar cuáles se pueden construir a partir del dataset existente.
- Documentar las consideraciones de negocio sobre cómo se calculan las métricas. Por ejemplo, algunas empresas calculan el revenue solo con órdenes en estado `entregado`, mientras que otras incluyen también `enviado`. Asegúrate de tener claridad en cada métrica y documenta los matices relevantes para que sean considerados durante el procesamiento con IA. `CLAUDE`
- Generar con IA el documento `findings_preliminary`: analizar los hallazgos, documentar las observaciones iniciales y las preguntas que surgen (`early_notes`).
- Realizar sesiones de discovery sobre los puntos más relevantes para el objetivo que quieres alcanzar. Un par de sesiones con alguien que conozca el dominio en profundidad mejorará significativamente la calidad de tus insights.

> **Tip:** Tómate el tiempo necesario para esta fase. Sentirse desorientado aquí es normal — es mucha información para un cerebro humano, pero no para la IA. Apóyate en ella para resolver dudas, generar queries rápidos o solicitar datos ya procesados. Todo va cobrando sentido a medida que pasas más tiempo con la data y construyes contexto.

---

## Fase 2 — Estrategia de datos: definir las preguntas de negocio

**Objetivo:** Definir las preguntas que el negocio debe responder, alineadas con la misión y la estrategia de la compañía. Luego construir y ejecutar los queries que las responden.

Tareas:
- Revisar la misión y la estrategia de la compañía para alinear cualquier estructuración de datos e insights con la dirección que el negocio persigue. En este caso, construí una misión y estrategia hipotéticas.
- A partir de `early_notes`, construir una lista de preguntas alineadas al tipo de producto y a la estrategia de la compañía (`business_questions`). Usa IA para descubrir preguntas que no habías considerado.
- Identificar las métricas de negocio relevantes para la industria del producto. Valida con IA cuáles se pueden construir a partir del dataset existente (`reference_metrics.md`).
- Construir los queries que responderán cada una de las `business_questions` basándose en el dataset.
- Responder todas las preguntas de negocio usando los queries construidos, y documentar los hallazgos, preguntas de seguimiento y brechas de datos identificadas (`business_questions.md`).

---

## Fase 3 — Dashboard en Data Studio

**Objetivo:** Materializar los hallazgos en un dashboard ejecutivo publicado en la nube.

Tareas:
- A partir de los queries construidos, generar con IA las vistas calculadas de BigQuery que facilitarán la conexión con Data Studio.
- Abrir Data Studio (lookerstudio.google.com) con la misma cuenta de Google.
- Conectar las siguientes vistas de BigQuery como fuentes de datos: `v_orders_enriched`, `v_order_lines`, `v_rfm_segments`, `v_cohort_retention`, `v_monthly_metrics`, `stock_alerts`, `executive_health`, `customer_funnel`, `abc_classification`, `country_performance`, `country_clienttype_performance`.
- Definir la estructura del dashboard en borrador para identificar el tipo de gráfica que mejor representa cada pieza de información:
  1. **Resumen ejecutivo** — KPIs principales (revenue, órdenes, AOV, clientes activos), tendencia mensual y mapa de revenue por país.
  2. **Órdenes y operaciones** — Total de órdenes, órdenes válidas, órdenes de los últimos 180 días, % entregadas, % en progreso, % con problemas, % canceladas, % devueltas. Rendimiento operativo por país, distribución de cancelaciones por país, órdenes mensuales por país.
  3. **Productos y catálogo** — Categorías principales, treemap por producto, análisis ABC, alertas de stock.
  4. **Crecimiento** — Crecimiento MoM, clientes nuevos vs. recurrentes, retención mes 1.
  5. **Retención y cohortes** — Revenue, AOV, tasa de churn, retención por cohorte, revenue recurrente vs. nuevos clientes, revenue por país, AOV por tipo de cliente.
  6. **Clientes** — Distribución de segmentos, heatmap de cohortes, lista de clientes en riesgo, distribución por tipo de usuario.
- Construir las páginas del dashboard siguiendo la estructura definida. Ver `docs/dashboard_design.md`.

---

## Fase 4 — Roadmap

**Objetivo:** Sintetizar los hallazgos y construir un roadmap de iniciativas priorizado.

Tareas:
- Proponer iniciativas accionables para la compañía a partir de los hallazgos.
- Priorizar las iniciativas según la estrategia de la compañía utilizando el framework ICE. (`business_roadmap.md`)

# Roadmap

Este roadmap te va a llevar, paso a paso, por el proceso que seguí para este análisis: desde la construcción técnica, pasando por el análisis de datos, hasta el resultado final. Te dará una mirada al proceso que realicé y te permitirá replicarlo si así lo deseas. Estoy feliz de responder cualquier pregunta o recibir feedback en cualquier momento; puedes contactarme a mi correo electrónico: dianamildred.dsgn@gmail.com.

---
## Setup y exploración (Foundation)

**Objetivo:** montar BigQuery, cargar los datos, hacer la primera exploración y contextualización.

Tareas:
- Crear cuenta de Google Cloud (gratis, sin tarjeta) y proyecto `tiendalatam-casestudy`. Seguir `docs/setup_bigquery.md` paso a paso.
- Activar BigQuery sandbox y crear el dataset `tiendalatam`.
- Cargar los CSVs de `data_expanded/` con autodetección de esquema.
- Generar con AI un plan de EDA y ejecutarlo. `sql/exploratory.sql`, 6 queries que dan el panorama general: volumen, fechas, distribución de status y productos top.
- Crear con AI un `product_growth_metrics_ref` para mapear el universo ideal de métricas según el tipo de producto y evaluar el potencial de la data existente.
- Documenta las consideraciones de negocio sobre cómo se calculan las métricas. Por ejemplo, algunas empresas calculan el revenue solo con órdenes en status `entregado`, otras incluyen también `enviado`. Asegúrate de tener claridad en cada métrica y documenta los matices relevantes para que sean tenidos en cuenta durante el procesamiento con AI. `CLAUDE`
- Generar con AI `findings_preliminary`: analiza los hallazgos, documenta las observaciones iniciales y las preguntas que surgen `early_notes`.
- Hacer discovery sobre los puntos que consideres mas relevantes para el objetivo al que quieres llegar, un par de sessiones con alguien que conozca en profundidad mejorara la calidad de tus insights

> **Tip:** Tómate el tiempo para este paso. Sentirse perdido aquí es normal, es mucha información para un cerebro humano, pero no para la AI. Apóyate en ella para resolver dudas, generar queries rápidos o pedir datos ya procesados. Todo va cobrando sentido a medida que pasas más tiempo con la data y construyes contexto.

---

## Data Strategy - definir Preguntas de negocio 

**Objetivo:** Definir las preguntas que el negocios debe responder en base a la mision y estrategia de la compañia. 

Tareas:
- Consultar la mission y estrategias que la compañia tiene para alinear caulquier estructuracion de data e insights que generen valor en la direccion de que la compañia busca. En este caso yo construi una mission y strategia hipotetica.
- Construye en base a `early_notes` una lista de preguntas que esten alineadas al tipo de producto y a la estrategia de la compania `business_questions`. Usa AI para encontrar preguntas que no te habias hecho antes
- Identificar las metricas de negocio para la industria del producto, con AI valida cuales puedes construir en base al dataset existente `reference_metrics.md`
- Construye los queries que van a responder a las `business_questions` basados en el dataset.

---

## Responder las preguntas de negocio

- Responder a todas las preguntas de negocio usando los queries construidos y documenta los hallazgos, preguntas y gaps que encuentras `business_questions.md`

## Dashboard en Data Studio

**Objetivo:** materializar los hallazgos en un dashboard ejecutivo publicado en la nube.

Tareas:
- En base a las queries construidas genera con AI las vistas calculadas de Bigquery que te van a ayudar facilitar las conexion con Data Studio.
- Abrir Data Studio (lookerstudio.google.com) con la misma cuenta de Google.
- Conectar como fuentes de datos las vistas que creamos en BigQuery: `v_orders_enriched`, `v_order_lines`, `v_rfm_segments`, `v_cohort_retention`, `v_monthly_metrics`, `stock_alerts`, `executive_health`, `customer_funnel`, `abc_classification`, `country_performance`, `country_clienttype_perfomance`.
- Definir la estructura del dashboard en borrador para entender el tipo de grafica que mejor representa la informacion que se quiere representar
1. **Overview — KPIs principales (Revenue, Órdenes, AOV, Clientes Activos), tendencia mensual y mapa de revenue por país.
2. **Orders and operations** - Total orders, valid orders, orders placed in the las 180 days, % delivered, % in progress, % problem orders, % cancelled, % returned. operational performance by country, cancellation distribution by country, montly orders by country. 
3. **Products aand catalog** — Top categorías, treemap por producto, ABC analysis, alertas de stock.
4. **Growth** — MoM growth, nuevos vs recurrentes, retención mes-1.
5. **Retention and cohorts** - Revenue AOV, churn rate, retention by cohort, revenue recurring vs new clients, revenue by country, AOV by client type.
6. **Clientes** — Distribución de segmentos, heatmap de cohortes, lista de clientes en riesgo, distribucion por tipo de usuario. 
- Contruir 8 paginas siguiendo la estructura definida `docs/dashboard_design.md`

## Roadmap

**Objetivo:** sintetizar los hallasgos y construir un roadmap priorizado.

Tareas:
- Proponer accionables para la compania en base a los hallazgos
- Priopriza los accionables en base a la estrategia de la compañia utilizando el framework ICE. `business_roadmap.d`

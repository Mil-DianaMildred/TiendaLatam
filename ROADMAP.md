# Roadmap

Este roadmap te va a llevar, paso a paso, por el proceso que seguí para este análisis: desde la construcción técnica, pasando por el análisis de datos, hasta el resultado final. Te dará una mirada al proceso que realicé y te permitirá replicarlo si así lo deseas. Estoy feliz de responder cualquier pregunta o recibir feedback en cualquier momento; puedes contactarme a mi correo electrónico: dianamildred.dsgn@gmail.com.

---
## Setup y exploración (Foundation)

**Objetivo:** montar BigQuery, cargar los datos, hacer la primera exploración y contextualización.

Tareas:
- Crear cuenta de Google Cloud (gratis, sin tarjeta) y proyecto `tiendalatam-casestudy`. Seguir `docs/setup_bigquery.md` paso a paso.
- Activar BigQuery sandbox y crear el dataset `tiendalatam`.
- Cargar los CSVs de `data_expanded/` con autodetección de esquema.
- Generar con AI un plan de EDA y ejecutarlo. `sql/exploratory.sql` — 6 queries que dan el panorama general: volumen, fechas, distribución de status y productos top.
- Crear con AI un `product_growth_metrics_ref` para mapear el universo ideal de métricas según el tipo de producto y evaluar el potencial de la data existente.
- Documenta las consideraciones de negocio sobre cómo se calculan las métricas. Por ejemplo, algunas empresas calculan el revenue solo con órdenes en status `entregado`, otras incluyen también `enviado`. Asegúrate de tener claridad en cada métrica y documenta los matices relevantes para que sean tenidos en cuenta durante el procesamiento con AI. `CLAUDE`
- Generar con AI `findings_preliminary`: analiza los hallazgos, documenta las observaciones iniciales y las preguntas que surgen `early_notes`.
- Hacer discovery sobre los puntos que consideres mas relevantes para el objetivo al que quieres llegar, un par de sessiones con alguien que conozca en profundidad mejorara la calidad de tus insights

> **Tip:** Tómate el tiempo para este paso. Sentirse perdido aquí es normal — es mucha información para un cerebro humano, pero no para la AI. Apóyate en ella para resolver dudas, generar queries rápidos o pedir datos ya procesados. Todo va cobrando sentido a medida que pasas más tiempo con la data y construyes contexto.

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

## Dashboard en Looker Studio

**Objetivo:** materializar los hallazgos en un dashboard ejecutivo publicado en la nube.

Tareas:
- En base a las queries construidas genera con AI las vistas calculadas de Bigquery que te van a ayudar facilitar las conexion con Looker studio.
- Abrir Looker Studio (lookerstudio.google.com) con la misma cuenta de Google.
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

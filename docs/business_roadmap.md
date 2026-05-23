# TiendaLatam — Suggested Action Plan Roadmap

[Dashboard access](https://datastudio.google.com/reporting/9dec01da-addc-4921-9df1-1bff8d7a887c)

## Matriz de Priorización ICE

> **North Star Metric:** Revenue mensual de clientes recurrentes (órdenes Enviado + Entregado)

**Framework ICE:** Impact × Confidence × Ease (escala 1–10, score máximo = 1.000)

- **Impact:** qué tanto mueve la North Star Metric (revenue mensual de recurrentes)
- **Confidence:** qué tan respaldada está la hipótesis por los datos disponibles
- **Ease:** inverso de costo/tiempo/complejidad de ejecución

---

### Tabla de priorización

| # | Iniciativa | Categoría | Fase | I | C | E | Score ICE |
|---|---|---|---|:---:|:---:|:---:|:---:|
| 1 | Protocolo de protección a 132 Champions | Retención | 1 — Inmediato | 10 | 9 | 8 | **720** |
| 2 | Reposición de emergencia: Laptop & Vacuum | Operaciones | 1 — Inmediato | 10 | 10 | 7 | **700** |
| 3 | Auditar cuello de botella Pendiente + Procesando | Operaciones | 1 — Inmediato | 9 | 9 | 6 | **486** |
| 4 | Activar 156 compradores únicos Retail | Clientes | 2 — Corto plazo | 8 | 8 | 8 | **512** |
| 5 | Campaña de rescate segmento At Risk | Retención | 2 — Corto plazo | 8 | 7 | 8 | **448** |
| 6 | Flujo de reactivación automático — día 50 | Retención | 2 — Corto plazo | 7 | 8 | 7 | **392** |
| 6 | Investigar cohortes Feb–May 2025 | Retención | 3 — Mediano plazo | 8 | 7 | 7 | **392** |
| 8 | Motor de adquisición para 64 no-compradores | Clientes | 3 — Mediano plazo | 6 | 7 | 6 | **252** |
| 9 | Escalar Ecuador como benchmark operacional | Expansión | 3 — Mediano plazo | 7 | 8 | 5 | **280** |
| 9 | Diagnóstico profundo de Colombia | Expansión | 2 — Corto plazo | 6 | 8 | 5 | **240** |
| 11 | Bundle Headphones + USB-C Charger | Catálogo | 2 — Corto plazo | 5 | 7 | 9 | **315** |
| 12 | Redefinir segmentación VIP y Wholesale | Clientes | 2 — Corto plazo | 5 | 6 | 6 | **180** |
| 13 | Revisión de catálogo: estrategia de diversificación | Catálogo | 3 — Mediano plazo | 7 | 6 | 4 | **168** |

---

## Phase 1 — Immediate (0–30 days)
*Put out the fires: critical risks that, if left unaddressed, erode the core business promise.*

### 🔴 Emergency Restock: Laptop and Vacuum
**Category:** Operations
> Ultralight Laptop at 30.8 days of stock remaining. Generates 33.2% of total revenue.

Issue an immediate purchase order for the 25 SKUs under alert. The reorder criterion must be documented and automated: restock trigger = 90 days of available inventory.

- **Owner:** Supply Chain
- **KPI:** Days of inventory ≥ 90d for top 5 SKUs

---

### 🔴 Audit the Pending + Processing Bottleneck
**Category:** Operations
> 646 orders in intermediate states = ~$316K of blocked GMV. 16.2% of all orders never advance on time.

Map the order-by-order flow for Pending and Processing statuses. Identify the bottleneck: is it payment validation, internal approval, or a failed integration with the distribution center? Top priority in Colombia (6.69% cancellation rate).

- **Owner:** Ops + Tech
- **KPI:** % orders in intermediate states < 5%

---

### 🔴 Protection Protocol for the 132 Champions
**Category:** Retention
> 132 customers = 56.4% of revenue. Losing 10 Champions hurts more than losing 100 new customers.

Pull the Champions list from the RFM dashboard. Assign a point of contact (account manager or automated CRM). Check if any has gone more than 60 days without a purchase and trigger a personalized intervention this week.

- **Owner:** CRM / Sales
- **KPI:** 0 Champions churned in the next 90 days

---

## Phase 2 — Short Term (30–90 days)
*Build the retention and growth engines: highest-impact initiatives on recurring revenue and the customer base.*

### 🟠 Automated Reactivation Flow — Day 50 Post-Purchase
**Category:** Retention
> Median time to second purchase: 74 days. Optimal intervention window is day 50–74. Conversion drops significantly after day 90.

Design an email/WhatsApp flow that automatically triggers on day 50 post-first-purchase for Retail customers. Message based on the category of the first purchase (smart cross-sell) with a clear price offer. Measure second-purchase rate before and after.

- **Owner:** CRM + Marketing
- **KPI:** % one-time buyers → second purchase within 74 days

---

### 🟠 Rescue Campaign for At Risk Segment
**Category:** Retention
> 64 At Risk customers with $160K in historical revenue. They have proven value and are declining — recoverable at low cost.

Direct (non-mass) outreach to all 64 At Risk customers with a personalized offer. Message acknowledges their history and presents a specific incentive: discount on their most-purchased category. Goal: convert at least 20 back to active.

- **Owner:** CRM
- **KPI:** % At Risk reactivated within 90 days

---

### 🟠 Deep-Dive Diagnosis of Colombia
**Category:** Expansion
> Colombia: $2,084/active month vs Ecuador's $3,372. Triple problem: lowest revenue, highest cancellation (6.69%), lowest AOV ($428). Same tenure as Mexico but a $40K gap.

Audit the Colombia distribution center operation: processing times, payment validation rate, product mix vs other countries. Deliverable: diagnosis with prioritized hypotheses and a 60-day intervention plan.

- **Owner:** Country Manager CO + Ops
- **KPI:** Revenue/active month Colombia ≥ $2,500

---

### 🟠 Launch Headphones + USB-C Charger Bundle
**Category:** Catalog
> The only co-purchase pair with clear product affinity: 23 orders together. Cross-sell is virtually inactive — max 30 co-purchases across 3,000 orders.

Create an explicit bundle in the cart with a combined price slightly below the sum of the individual items. Measure whether the bundle increases AOV on orders that include either product. Low risk, executable in 2 weeks.

- **Owner:** Product + Catalog
- **KPI:** AOV on orders with tech + accessory products

---

### 🟠 Activate the 156 Retail One-Time Buyers
**Category:** Customers
> 39.8% of Retail customers bought only once. Converting even 20% of them to regular buyers generates ~$50K in estimated incremental revenue.

Segment the 156 one-time buyers by time since first purchase. For those who bought within the last 90 days: immediate reactivation flow (see day-50 flow). For older ones: re-engagement campaign with a tiered incentive (more generous the longer they've been inactive).

- **Owner:** CRM
- **KPI:** % one-time → second purchase within 60 days

---

### 🟠 Define Real Segmentation Criteria for VIP and Wholesale
**Category:** Customers
> VIP has lower LTV than Retail. Wholesale buys the same volume and frequency as Retail. Segments are labels with no differential behavior.

Internal workshop with Sales and CRM to redefine tier assignment criteria. Proposal: 2 entry segments (Consumer and B2B) with clear conditions for moving up. Each tier must have at least one measurable exclusive benefit (volume discount, priority stock access, payment terms).

- **Owner:** Product + Sales
- **KPI:** LTV spread between tiers ≥ 30%

---

## Phase 3 — Medium Term (90–180 days)
*Diversify and scale: reduce dependency on Technology and prepare expansion in key markets.*

### 🔵 Catalog Review: Diversification Strategy
**Category:** Catalog
> Technology alone drives 54.75% of revenue on the back of just 2 SKUs. Home and Fashion have comparable demand volume but 3–6x less revenue due to low unit prices.

Run a structured catalog review to decide where to grow next: evaluate adding higher-ticket SKUs in underpenetrated categories, expanding into new ones, or doubling down on existing strengths. Decision should be grounded in demand signals from the data, competitive pricing research, and sourcing feasibility — before committing to any specific SKUs.

- **Owner:** Catalog + Purchasing
- **KPI:** % revenue from non-Tech categories increasing QoQ

---

### 🔵 Scale Ecuador as the Operational Benchmark
**Category:** Expansion
> Ecuador leads in revenue/active month ($3,372), lowest cancellation (3.75%), and highest delivery rate (66.6%). It's the internal benchmark for all 9 other markets.

Document Ecuador's distribution center processes: processing times, payment validation flow, catalog mix. Use this as the operational benchmark and migration plan for Bolivia and Peru (the next best performers on the list).

- **Owner:** Ops + Country Managers
- **KPI:** Global delivery rate ≥ 72%

---

### 🔵 Build an Acquisition Engine for 64 Registered Non-Buyers
**Category:** Customers
> 64 registered customers who never purchased (9.1%). This is an activation problem, not a demand problem. New customers per month (15–39) remains low for the business scale.

Design a post-registration onboarding flow: welcome email with a time-limited first-purchase offer (urgency), followed by reminders at day 7 and day 14. Measure registration → first purchase conversion. In parallel, explore organic acquisition channels (SEO, referrals) to grow the base without relying solely on paid.

- **Owner:** Growth + CRM
- **KPI:** Activation rate (registration → first purchase) ≥ 70%

---

### 🔵 Investigate What Changed in the Feb–May 2025 Cohorts
**Category:** Retention
> Feb–May 2025 cohorts are the best in the dataset: Q1 retention of 33–54% and Q3 retention of 38–62%. Something significantly improved in that period.

Review what changed between Dec 2024 and Mar 2025: catalog launches, price changes, operational improvements, marketing campaigns. The goal is to identify the cause and deliberately replicate it across all markets.

- **Owner:** PM + Data
- **KPI:** Average Q1 retention ≥ 35% in future cohorts

---

## Summary Table

| Initiative | Category | Phase | Owner | KPI |
|---|---|---|---|---|
| Emergency restock: Laptop & Vacuum | Operations | 1 — Immediate | Supply Chain | Inventory ≥ 90d for top 5 SKUs |
| Audit Pending + Processing bottleneck | Operations | 1 — Immediate | Ops + Tech | Intermediate orders < 5% |
| Protection protocol for 132 Champions | Retention | 1 — Immediate | CRM / Sales | 0 Champions churned in 90d |
| Reactivation flow — day 50 | Retention | 2 — Short term | CRM + Marketing | % one-time → 2nd purchase < 74d |
| Rescue campaign for At Risk | Retention | 2 — Short term | CRM | % At Risk reactivated in 90d |
| Colombia deep-dive diagnosis | Expansion | 2 — Short term | Country Manager CO | Revenue/month ≥ $2,500 |
| Headphones + USB-C bundle | Catalog | 2 — Short term | Product + Catalog | AOV on tech + accessories |
| Activate 156 one-time buyers | Customers | 2 — Short term | CRM | % one-time → 2nd purchase < 60d |
| Redefine VIP & Wholesale segmentation | Customers | 2 — Short term | Product + Sales | LTV spread between tiers ≥ 30% |
| Catalog review: diversification strategy | Catalog | 3 — Medium term | Catalog + Purchasing | Non-Tech revenue % increasing QoQ |
| Scale Ecuador as benchmark | Expansion | 3 — Medium term | Ops + Country Managers | Global delivery rate ≥ 72% |
| Acquisition engine for non-buyers | Customers | 3 — Medium term | Growth + CRM | Activation rate ≥ 70% |
| Investigate Feb–May 2025 cohorts | Retention | 3 — Medium term | PM + Data | Q1 retention ≥ 35% in new cohorts |

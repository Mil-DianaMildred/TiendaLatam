# Hallazgos preliminares (resultados reales de las queries)

Estos números los obtuvimos ejecutando las queries del proyecto contra los CSVs. Te sirven como teaser para escribir el caso de estudio y como sanity check de tu pipeline. Cuando montes la base en Power BI deberías llegar a los mismos resultados (las pequeñas diferencias entre Postgres y un cálculo en pandas son normales por manejo de quartiles).

## Métricas globales (órdenes status 3 o 4)

- Revenue total: **$128,406.25**
- Órdenes válidas: **300**
- Clientes compradores únicos: **129**
- AOV: **$428.02**
- Ventana de análisis: junio 2022 → abril 2026

## Top 5 países (por revenue)

| País | Órdenes | Revenue | AOV |
|------|---------|---------|------|
| Uruguay | 22 | $15,466.2 | **$703.01** |
| Brasil | 28 | $13,274.3 | $573.6 |
| Perú | 24 | $13,766.3 | $494 |
| Ecuador | 23 | $9,113.2	| $396.23 |
| Costa Rica | 17	| $8,662.15	| $509.54 |

Insight: **Uruguay tiene el AOV más alto** (~$300 sobre la media). Hipótesis: mejor mix de cliente Mayorista/Corporativo o productos de mayor ticket. Pregunta para el caso: ¿es replicable a otros países?

## Bottom 3 países

| País | Órdenes | Revenue | AOV |
|------|---------|---------|------|
| Bolivia	| 13	| $4,778.8	| $367.6 |
| México	| 18	| $2,810.5	| $156.14 |
| Chile	| 12	| $2,463.0	| **$205.25** |

Insight: **México tiene volumen aceptable pero AOV bajo**. Posible oportunidad de upselling o revisión del mix de catálogo.

## Segmentación RFM (el insight estrella)

| Segmento | Clientes | Revenue | % Revenue |
|----------|----------|---------|-----------|
| **Champions**	| **25**	| **$41,255.0**	| **39.7** |
| Needs Attention	| 17	| $22,201.0	| 21.4 |
| Loyal	32 |	19,239.0	| $18.5 |
| At Risk	| 7	| 9,453.0	| $9.1 |
| Lost	| 17	| 4538.0	| $4.4 |
| Hibernating	| 5	| $4,119.0	| 4.0 |
| About to Sleep |	12	| $3,148.0	| 3.0 |

Insight principal del proyecto: **25 clientes (~25% de la base activa) generan el 40% del revenue**. La regla de Pareto se cumple ligeramente sub-amplificada porque el dataset es relativamente joven y pequeño.

Insight secundario: **At Risk + Hibernating + Lost = 24 clientes que ya generaron $14,000 en revenue histórico y hoy no están comprando**. Esa es la oportunidad de retención más clara del negocio.

## Salud del funnel

- **Churn rate (180+ días sin comprar)**: **44.7%**
- **Clientes registrados que nunca compraron**: **35 de 150 (23%)** — bandera roja, hay un problema de activación.
- **Time-to-second-purchase**: mediana de **163 días** (5+ meses). Esto es altísimo. Implicación PM: una campaña de re-engagement a los 30-60 días podría ser muy efectiva.

## 3 recomendaciones de producto candidatas (para el caso de estudio)

Estas son las que sugiero llevar al storytelling, ya priorizadas con criterio ICE (Impact, Confidence, Ease, escala 1-10):

| Recomendación | I | C | E | ICE | Justificación |
|---------------|---|---|---|-----|----------------|
| **1. Programa de fidelización para Champions** | 9 | 8 | 6 | 432 | 26 clientes mueven 40% del revenue. Pequeñas mejoras de retención aquí mueven mucha aguja. |
| **2. Campaña de reactivación At Risk + Hibernating** | 8 | 7 | 8 | 448 | 21 clientes con LTV histórico de ~$16K. Email/llamada del Asesor Comercial = costo bajísimo. |
| **3. Onboarding mejorado para nueva compra** | 7 | 6 | 7 | 294 | Reducir time-to-2nd-purchase de 163d a <90d. Cupón post-primera-compra + welcome series. |

Cuando hagas la presentación, justifica cada score y di explícitamente qué métrica esperarías mover (ej: "espero subir retención mes-3 de X% a Y%").

## Sanity checks que vale la pena revisar manualmente

- 35 clientes registrados sin órdenes: ¿son data dummy o realmente fallaron en activar?
- AOV de Uruguay vs México: cruzar con tipo de cliente y categoría dominante.
- Diciembre 2025 mostró +94% MoM y enero 2026 -77%. Estacionalidad típica de Q4. Vale la pena visualizarlo año contra año en el dashboard.

# TiendaLatam — Insights Organizados

**Misión:** *"Que cualquier latinoamericano pueda comprar productos de calidad al mejor precio del mercado, sin depender de lo que ofrece el comercio local."*

**Estrategia:** Ganar en precio → retener digitalmente → expandir donde el diferencial de precio duele más → diversificar catálogo para no depender de Tecnología.

[Dashboard access](https://datastudio.google.com/reporting/9dec01da-addc-4921-9df1-1bff8d7a887c)

---

## 1. General

Contexto de negocio y salud operativa global.

**Volumen y ventana de tiempo (E1)**

- En casi 5 años de operación TiendaLatam procesó 4,000 órdenes con $1.47M de revenue. El punto de inflexión fue 2024–2025: el negocio triplicó en un año ($205K → $607K), y 2026 con solo 4 meses ya acumula $574K.
- El 76.12% de las órdenes genera revenue real (3,045/4,000). El 23.88% restante corresponde a cancelaciones, devoluciones y órdenes en proceso.
- 64 de 700 clientes registrados nunca compraron (9.1%) — señal de un problema de activación, no de demanda.
- El AOV de $489 es sólido para e-commerce generalista en LATAM, donde el promedio del sector ronda los $300–$500.

**Salud operativa (E2 / E2b)**

- La tasa de entrega del 63.5% está 17–22 puntos porcentuales por debajo del benchmark regional para operadores maduros (80–85%).
- El 16.2% de órdenes en estados intermedios (Procesando 8.8% + Pendiente 7.4%) es el cuello de botella operativo más claro. Un operador eficiente debería tener este número por debajo del 5%.
- Cancelado (5.1%) + Devuelto (2.6%) = 7.7% — dentro del umbral de alerta del 10%, pero Colombia eleva esta cifra a 9.37% a nivel individual.
- TiendaLatam está en categoría "Malo" en 4 de 6 métricas operativas. El único indicador positivo estructural es la tasa de devolución (2.6% vs benchmark 20%) — el cliente que recibe el producto queda satisfecho. El problema no es la calidad del producto, es llegar a entregarlo.
- La brecha GMV → revenue ($485K, 24.78%) se descompone en: 7.7% de pérdida definitiva ($150K) y 16.2% de revenue atrapado en órdenes en proceso o pendientes (~$317K).

---

## 2. Revenue & Finance

Crecimiento, AOV, nuevos vs recurrentes, y desempeño por segmento de cliente.

**Crecimiento anual (A3-Q11)**

- El negocio creció ininterrumpidamente desde 2021. El punto de inflexión fue 2024–2025: en un año el revenue se triplicó ($205K → $607K).
- 2026 con solo 4 meses ya acumula $574K — si la tendencia se mantiene, el año cerraría por encima de $1.5M, más del doble de 2025.
- El crecimiento no proviene de adquisición masiva sino de la acumulación de clientes recurrentes. El negocio está escalando sobre su base existente.

| Año | Revenue | Crecimiento YoY |
|---|---|---|
| 2023 | $71,700 | +449% |
| 2024 | $205,382 | +187% |
| 2025 | $607,340 | +196% |
| 2026 (4 meses) | $574,782 | — |

**Nuevos vs recurrentes (A2-Q10)**

- Los últimos 12 meses muestran que el 79–89% del revenue viene de clientes recurrentes — el negocio está madurando y ya no depende de adquisición constante.
- Noviembre–Diciembre 2025 son los meses con más revenue de recurrentes ($100K y $114K) — confirma la estacionalidad navideña como el pico más importante del año.
- Abril 2026 es el mejor mes del dataset ($220K total) con $143K de recurrentes — señal de aceleración del negocio.
- El número absoluto de clientes nuevos por mes (15–39) es bajo para la escala del negocio. La adquisición sigue siendo la palanca de crecimiento pendiente.

**LTV por segmento (A2-Q9)**

- El spread entre el LTV más alto (Corporativo $2,425) y el más bajo (Mayorista $1,999) es de apenas 17%. Para un negocio con 4 tipos de cliente tan distintos, ese rango es casi plano — señal de que no hay diferenciación real de propuesta de valor entre segmentos.
- VIP ($2,347) tiene el tercer LTV más bajo, por debajo del Minorista ($2,387). Si existe una categoría VIP, debería tener el LTV más alto con diferencia.
- Mayorista ($1,999) con solo 4.47 órdenes promedio: el segmento que por definición debería comprar en volumen está comprando igual que un minorista.

**AOV por segmento (A3-Q13)**

- Mirando los últimos 4 trimestres (Q3 2024 – Q2 2026), los cuatro segmentos operan en el mismo rango de ticket promedio ($390–$790). La convergencia es la señal más crítica del análisis de segmentación.
- Mayorista: AOV reciente ($392–$441) es el más bajo del grupo — el segmento que por definición debería comprar en volumen está comprando igual que un minorista.
- VIP: el segmento "premium" no se comporta como tal en ticket promedio. Sin beneficios exclusivos que incentiven mayor gasto, la etiqueta VIP es cosmética.
- Corporativo: tiene el mayor potencial de crecimiento de AOV — contratos y pricing especial por volumen son la palanca más directa.

---

## 3. Orders & Operations

Fulfillment, cuellos de botella, y performance por país.

**Cuello de botella operativo (A2-Q9b)**

- 646 órdenes en estados intermedios representan aproximadamente $316K de GMV bloqueado (asumiendo AOV de $489).
- Un cliente cuya primera orden queda en "Pendiente" tiene menor probabilidad de hacer una segunda compra — el primer ciclo de compra nunca se completó satisfactoriamente.
- El dataset no contiene timestamps de cambio de estado — no es posible medir cuánto tiempo lleva una orden en cada estado. Fuente sugerida: sistema OMS.

**Performance por país (A3-Q11b / A3-Q12)**

- Hay 16 meses de diferencia entre el primer mercado (Ecuador, jul 2021) y el último (Argentina, nov 2022). La comparación de revenue absoluto sin considerar esto puede llevar a priorizar mal.
- Colombia y México se lanzaron el mismo mes (jul–ago 2022, 46 meses activos), pero Colombia ($95K) está muy por debajo de México ($136K). La brecha no se explica por madurez — Colombia tiene un problema específico.
- La métrica de comparación justa es revenue por mes activo: Ecuador ~$3,372/mes, Perú ~$3,668/mes, Colombia ~$2,084/mes. Colombia underperforma incluso ajustado por tiempo.
- Ecuador es el mercado modelo: lidera en revenue, AOV sólido ($505), cancelación más baja (3.75%) y tasa de entrega más alta (66.6%).
- Colombia tiene el triple problema: menor revenue ($95K), mayor cancelación (6.69%) y menor AOV ($428). No es un problema de un solo factor — es un diagnóstico combinado operativo-comercial.
- Argentina destaca por AOV ($563) con solo 61 compradores — es un mercado de nicho de alto valor, no de volumen.
- Brasil y México comparten perfil: revenue medio-bajo, AOV por debajo del promedio ($426–$468), cancelación 5.15–5.47%. La operación en ambos mercados no está lista para escalar de forma rentable.

---

## 4. Products & Catalog

Concentración de SKUs, riesgo de quiebre de stock, co-purchase y diversificación.

**Curva ABC y concentración (A1-Q1 / E4)**

- 2 SKUs (Laptop Ultraliviana + Smartphone Andino) acumulan el 46.2% del revenue total. Esta concentración es el mayor riesgo sistémico del negocio.
- Curva ABC: Categoría A (≥80% del revenue) = 17 de 50 productos. Categoría C (los últimos 33 SKUs) representa menos del 20% — no hay exceso de long tail.
- Tecnología sola (54.75%) supera la suma de las otras 7 categorías (45.25%). El riesgo está más concentrado de lo que el número de categoría sugiere.
- El top 10 por unidades tiene volúmenes muy similares (599–673 unidades) — el diferencial de revenue viene del precio unitario, no del volumen.

**Riesgo de quiebre de stock (A1-Q2)**

- Alerta crítica: la Laptop Ultraliviana 14 — el SKU que genera el 33.2% del revenue — tiene 64 unidades en stock y solo 30.8 días de inventario.
- La Aspiradora Compacta (55 unidades, 28.4 días) es el segundo en mayor riesgo y el tercer SKU por revenue ($88K).
- 25 de 50 productos (50% del catálogo) están en alerta simultáneamente — indica un problema sistémico de reabastecimiento, no casos aislados.
- En un modelo de distribución propia, el quiebre de stock no tiene red de seguridad: si no está en bodega, el cliente va al comercio local, lo que contradice la promesa de precio.

**Co-purchase y cross-sell (A1-Q3)**

- La mayoría de las combinaciones con mayor co-purchase cruzan categorías no relacionadas (Parlante + Shampoo, Cinturón + Shampoo) — reflejan compras de múltiples necesidades en una sola sesión, no afinidad de producto.
- El único par de afinidad lógica clara: Audífonos Bluetooth + Cargador USB-C (23 órdenes) — base concreta para un bundle de tecnología portable.
- El volumen máximo de co-purchase (30 órdenes) sobre ~3,000 órdenes totales indica que el cross-sell está prácticamente desactivado.
- Laptop + Bloques de Construcción (23 co-purchases) sugiere que el comprador adquiere para toda la familia en una sola orden.

**Diversificación de catálogo (A4-Q14)**

- Hogar y Moda tienen volúmenes de órdenes comparables a Tecnología (~4,000 unidades) pero revenue entre 3x y 6x menor, por precio promedio bajo ($60 Hogar, $36 Moda). La demanda existe — el gap es de precio y propuesta de valor.
- Para reducir Tecnología del 54.75% sin que caiga el revenue total, Hogar necesita crecer de $244K a ~$350K. Eso requiere subir el precio promedio por unidad, no solo el volumen.
- Alimentos y Papelería son categorías de frecuencia con precio promedio de $7–$8/unidad. Su rol estratégico es acortar el tiempo entre pedidos, no mover el ticket promedio.
- Ningún SKU del catálogo tiene cero ventas — todos se venden. El problema en Alimentos y Papelería es precio unitario tan bajo ($3.60–$6.75) que la contribución al revenue es marginal.

---

## 5. Retention & Cohorts

Comportamiento de recompra, cohortes, churn y ventana de intervención.

**Cohortes mensuales (A2-Q4)**

- Las cohortes de 2021–2022 son estadísticamente muy pequeñas (1–4 clientes) y no son concluyentes. Las primeras cohortes con masa crítica aparecen desde 2023.
- Las cohortes de 2024–2025 muestran retención Q1 del 20–54%, significativamente mejor que las de 2023 (10–25%). Hay señal de mejora sostenida del producto o la experiencia.
- El patrón de retención no es inmediato: los clientes que vuelven lo hacen predominantemente en Q2 o Q3, no en el primer mes. La ventana de intervención óptima es entre los días 50 y 74.
- Las cohortes de 2025 Feb–May son las mejores del dataset — retención Q1 del 33–54% y retención a 3 trimestres del 38–62%. Investigar qué cambió en ese período es una prioridad analítica.

**Tiempo a la segunda compra (A2-Q8)**

- 389 de 636 compradores (61.2%) realizaron una segunda compra — base recurrente sólida, pero el 38.8% restante son clientes potencialmente perdidos.
- La mediana de 74 días define la ventana de intervención: la campaña de reactivación para Minoristas debe salir entre el día 50 y el día 74 post-primera compra. Después del día 90 la tasa de conversión cae significativamente.
- VIP recompra antes (mediana 52 días) — probablemente tiene una necesidad estructurada. Mayorista es el más lento (89 días) — posiblemente compra en ciclos de inventario.
- La media (132 días) muy superior a la mediana (74 días) revela un grupo de clientes con ciclos de recompra muy largos (hasta 1,229 días) que eventualmente caen en churn si no hay intervención.

**Churn por segmento (A2-Q7)**

- El churn global del 23% en un negocio de 5 años es alto. El benchmark en e-commerce LATAM maduro se sitúa en el 15–20%.
- Minorista tiene el mayor churn (26.3%) siendo el segmento que sostiene el negocio — este es el hallazgo más preocupante del análisis de retención.
- El spread entre segmentos es pequeño (23–26.3%) — no hay un tipo de cliente que retenga significativamente mejor, lo que apunta a un problema sistémico de experiencia o propuesta de valor.

**Segmento RFM (A2-Q6)**

- 132 clientes (20.8% de la base activa) generan el 56.4% del revenue — concentración más extrema que la regla 80/20 clásica.
- Champions + Loyal (241 clientes, 37.9% de la base) acumulan el 76.4% del revenue. Este núcleo es el activo más valioso del negocio y también su mayor fragilidad.
- At Risk (64 clientes, $160K revenue histórico) es el segmento de acción más urgente: tienen valor probado y actividad reciente decayendo. Son rescatables con bajo costo relativo.
- Lost (146 clientes) es el grupo más numeroso pero con el menor revenue histórico por cliente ($238 promedio). Candidatos a reactivación solo si el costo de campaña es marginal.

---

## 6. Customers

Perfil del ICP, segmentación, y valor por tipo de cliente.

**Distribución de clientes (E3)**

- La distribución del tipo de cliente es casi idéntica en los 10 países — no hay sobre-indexación geográfica de ningún segmento. El mix de adquisición no está diferenciado por mercado.
- El Minorista domina no por mayor frecuencia de compra sino por volumen: 392 clientes vs 74 Corporativos y 52 VIPs.
- La frecuencia promedio es prácticamente igual en los cuatro tipos (4.5–4.9 órdenes/cliente) — anomalía en un negocio con segmentos B2C y B2B, donde los B2B deberían comprar con más cadencia.

| Tipo | Clientes | Revenue | % Revenue |
|---|---|---|---|
| Minorista | 392 | $935,941 | 63.5% |
| Mayorista | 118 | $235,986 | 16.0% |
| Corporativo | 74 | $179,496 | 12.2% |
| VIP | 52 | $122,074 | 8.3% |

**ICP real — el Minorista Power Buyer (E6)**

- El ICP real no es "el Minorista" — es el Minorista Power Buyer: 71 clientes (18.1% del segmento) que generan aproximadamente el 57% del revenue Minorista con un LTV de $7,592 y 17 órdenes promedio.
- El 39.8% de Minoristas solo compró una vez. Convertir estos 156 one-time buyers a compradores regulares es la palanca de activación de mayor volumen disponible.
- Con el 63.5% del revenue y la base más grande, el Minorista sostiene la operación y es el cliente más alineado con la misión declarada.

**Segmentación VIP y Corporativo (A2-Q9c)**

- VIP + Corporativo: 136 clientes, 20.46% del revenue. LTV promedio prácticamente igual al del Minorista — la diferencia entre Corporativo ($2,425) y Minorista ($2,387) es menor al 2%.
- Los datos no respaldan una inversión desproporcionada en adquisición de Corporativos o VIPs. Su LTV unitario no justifica el costo de atención diferenciada que estos segmentos típicamente requieren.
- La decisión estratégica más coherente con la misión: el foco debe estar en Minoristas — especialmente en convertir los 156 one-time buyers a regulares y proteger a los 71 Power Buyers.
- Si la segmentación actual no tiene criterios de asignación claros y medibles, la primera acción es redefinirla. Los segmentos sin beneficios diferenciados no son segmentos reales.

---

## Resumen ejecutivo — Hallazgos clave

| Pregunta | Hallazgo principal | Recomendación |
|---|---|---|
| E2b — Operación | Tasa de entrega 63.5% vs benchmark 80–85%; 4 de 6 métricas por debajo del estándar LATAM | Reducir estados intermedios (16.2% en Pendiente + Procesando) como prioridad #1 operativa |
| A1-Q1 — Catálogo | 2 SKUs = 46.2% del revenue; Laptop a 30.8 días de quiebre de stock | Proteger stock de Laptop + Smartphone; buscar SKUs de Categoría A en Hogar |
| A2-Q4 — Cohortes | Cohortes 2025 muestran retención Q1 del 33–54% — mejora sostenida frente al 10–20% de 2023 | Identificar qué cambió en 2025 Feb–May y replicarlo |
| A2-Q7 — Churn | Churn 23% global; Minoristas churnan al 26.3% | Flujo de reactivación al día 50 post-compra para Minoristas; protocolo para los 132 Champions |
| A2-Q9c — Segmentos | LTV spread entre segmentos solo 17%; VIP tiene LTV menor que Minorista | Redefinir segmentación con beneficios medibles o simplificar a 2 segmentos |
| A3-Q11b — Expansión | Revenue/mes activo: Ecuador $3,372 vs Colombia $2,084 | Diagnóstico específico de Colombia antes de cualquier inversión en adquisición |
| A4-Q14 — Catálogo | Hogar y Moda tienen ~4,000 unidades vendidas pero 3–6x menos revenue por precio bajo | Incorporar SKUs de mayor ticket en Hogar (>$100) y Moda (>$60) |

**North Star Metric recomendada:** Revenue mensual de clientes recurrentes (órdenes Enviado + Entregado).

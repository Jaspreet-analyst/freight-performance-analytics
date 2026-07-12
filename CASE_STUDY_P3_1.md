# 🌐 Case Study: Global Freight Performance & Customer Impact Analytics

**Author:** Jaspreet Singh | CEVA Logistics — Greater Toronto Area
**Tools:** MySQL · Tableau Public · GitHub
**Dataset:** 7 relational tables | 7,590 rows | 2022–2024
**Live Dashboard:** [View on Tableau Public](https://public.tableau.com/app/profile/jaspreet.singh5400/viz/GlobalFreightPerformanceCustomerImpactAnalytics/GlobalFreightPerformanceCustomerImpact20222024)
**GitHub Repo:** [freight-performance-analytics](https://github.com/Jaspreet-analyst/freight-performance-analytics)

---

## 🧩 The Problem

After 8+ years in ocean freight operations at CEVA Logistics, I noticed a pattern that no one was measuring — the direct connection between how we route shipments, which carriers we choose, and whether our customers stay or leave.

Customers were experiencing delays. Costs were higher than they needed to be. And nobody had a data model that connected all three dimensions — cost, speed and customer impact — in one place.

The questions nobody could answer with data:

- How much more does a transshipment route cost vs a direct route on the same lane?
- Which carriers consistently underperform against their contracted transit times?
- Which customers are at churn risk right now because of our service failures?
- If we optimize routing on our top 10 lanes, what is the projected annual saving?

This project was built to answer all four.

---

## 🎯 Objective

Build an end-to-end analytics model that connects freight operations data to customer impact — and quantifies the financial benefit of route optimization, better carrier selection and proactive customer retention.

---

## 🗄️ The Dataset

Seven interconnected tables were designed to mirror real 3PL operations:

| Table | Rows | Purpose |
|---|---|---|
| `carriers` | 10 | Contract rates, OTD scores, free days, negotiation status |
| `routes_fixed` | 60 | Direct vs transshipment routes — same lanes, different routing |
| `customers` | 50 | Segment, churn risk, NPS score, contract filing status |
| `shipments_p3` | 2,000 | Every shipment — route type, carrier, delay, on-time flag |
| `freight_costs` | 2,000 | Full landed cost breakdown including transshipment fees |
| `transit_performance` | 2,000 | Sailing, port wait, customs and transshipment wait days |
| `route_optimization_fixed` | 30 | Before vs after — days saved, cost saved, satisfaction lift |

**Total: 7,590 rows across 7 tables**

The `route_optimization_fixed` table is the most unique element of this project — it captures the actual results of route optimization decisions, showing exactly what changed and what was saved on each trade lane.

---

## 🔍 Methodology

### Step 1 — Database Design
Designed a 7-table relational schema in MySQL with shipments_p3 as the central fact table. Every other table connects through either Shipment ID, Carrier ID or Customer ID — mirroring how data lives in enterprise TMS systems like CargoWise and Oracle OTM.

### Step 2 — SQL Analysis (13 Queries across 3 levels)

**Level 1 — Route & Carrier Performance**
Used multi-table JOINs to compare direct vs transshipment routes on cost, transit time and on-time delivery. Built a carrier scorecard combining cost per container, actual transit days and OTD percentage into one view. Identified routes with the highest transshipment count and worst delay performance — flagging them as optimization priorities.

**Level 2 — Customer Impact Analysis**
Used CTEs to link delivery performance directly to customer churn risk. Calculated total annual spend at risk by combining delay data with customer annual spend values. Used correlated subqueries to identify carriers performing worse than the network average — providing data for carrier performance conversations.

**Level 3 — Route Optimization & Window Functions**
Applied RANK() OVER with PARTITION BY to identify the cheapest reliable carrier on each specific trade lane. Used window functions to calculate transit efficiency scores across all carriers. Built a nested CTE customer risk scorecard combining shipment performance, cost data and churn risk into one executive view with action priorities.

### Step 3 — Tableau Dashboard
Built a 7-chart interactive dashboard telling a complete story:
- Transit comparison — direct vs transshipment
- On-time distribution — pie chart
- Delay reasons — treemap
- Transit by carrier — bar chart
- OTD by carrier — stacked bar
- Route optimization results — before vs after
- Projected annual savings by lane

---

## 📊 Key Findings

### Finding 1 — Transshipment Routes Add 6–12 Days Per Shipment
Direct routes consistently outperform transshipment routes on transit time. The gap is not marginal — transshipment routes average 6 to 12 additional days per shipment depending on the lane. On high-frequency lanes this compounds into weeks of cumulative delay per year.

### Finding 2 — Transshipment Fees Are a Hidden Cost Driver
When the full cost breakdown is analyzed, transshipment fees emerge as a significant and often overlooked line item. These fees are paid per container per transshipment port — meaning a shipment moving through two transshipment ports pays the fee twice. Switching to direct routing eliminates this cost entirely.

### Finding 3 — Carrier Performance Varies Significantly vs Contracted Rates
Several carriers show a meaningful gap between their contracted on-time delivery rate and their actual performance in our data. This gap is the foundation of every carrier renegotiation conversation — and without data, these conversations are impossible to win.

### Finding 4 — Route Optimization Delivers Measurable Annual Savings
The route optimization analysis shows that switching from transshipment to direct routing on the top 10 lanes generates projected annual savings ranging from $50,000 to over $500,000 per lane depending on volume. Across all optimized lanes the total projected saving is significant.

### Finding 5 — High Churn Risk Customers Correlate With High Delay Rates
Customers flagged as High churn risk consistently show higher average delay days than Low risk customers. This is not coincidence — it is causation. Late deliveries erode trust, and eroded trust becomes churn. Filing contracts with these customers and prioritizing their shipments on direct routes is the most direct intervention available.

### Finding 6 — Port Congestion and Transshipment Delays Are Top Bottlenecks
The delay reasons treemap shows Port Congestion and Transshipment Delay as the two largest contributors to shipment delays. Both are addressable — port congestion through route diversification and transshipment delays through direct routing.

---

## 💡 Business Recommendations

| Recommendation | Action | Expected Impact |
|---|---|---|
| Switch top 10 transshipment lanes to direct routing | File new contracts with direct service carriers | 6–12 days saved per shipment |
| Renegotiate SLAs with underperforming carriers | Use carrier scorecard as negotiation evidence | Improved OTD or cost reduction |
| File contracts for all High churn risk customers | Guarantee space and rates for priority accounts | Reduced last-minute spot bookings |
| Eliminate double-transshipment routes | Audit all routes with 2+ transshipment ports | Direct cost reduction per container |
| Pull forward bookings on peak season lanes | Use monthly cost trend to identify surge months | Avoid peak season surcharges |
| Build carrier performance review cadence | Quarterly scorecard review with carrier reps | Accountability and continuous improvement |

---

## 🛠️ Skills Demonstrated

| Skill | Evidence |
|---|---|
| Relational Database Design | 7-table schema with primary and foreign keys |
| SQL — Multi-Table JOINs | 3-table JOINs across carriers, shipments and costs |
| SQL — CTEs | Single and nested CTEs for customer risk analysis |
| SQL — Window Functions | RANK() OVER, PARTITION BY lane, transit efficiency scoring |
| Data Visualization | 7-chart Tableau dashboard with treemap and pie chart |
| Supply Chain Domain | Route optimization, carrier negotiations, D&D, 3PL operations |
| Business Storytelling | Before vs after optimization with projected dollar savings |
| Customer Analytics | Churn risk linked to operational performance |

---

## 🔗 Project Links

- 📊 **Live Dashboard:** [Tableau Public](https://public.tableau.com/app/profile/jaspreet.singh5400/viz/GlobalFreightPerformanceCustomerImpactAnalytics/GlobalFreightPerformanceCustomerImpact20222024)
- 💻 **SQL Queries + Dataset:** [GitHub Repository](https://github.com/Jaspreet-analyst/freight-performance-analytics)
- 🔗 **Project 1:** [Ocean Freight SQL Analytics](https://github.com/Jaspreet-analyst/ocean-freight-sql-analytics)
- 🔗 **Project 2:** [Supply Chain Risk & Cost Analytics](https://github.com/Jaspreet-analyst/supply-chain-risk-analytics)

---

*Jaspreet Singh | Ocean Import Coordinator | CEVA Logistics | Greater Toronto Area*
*8+ years across ocean import, air freight, carrier negotiations, D&D cost recovery, pharma cold chain and key account operations*
*CIFFA Certified · FIATA Diploma in Freight Forwarding (June 2026)*

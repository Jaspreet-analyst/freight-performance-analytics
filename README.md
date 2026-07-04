<div align="center">

<img width="100%" src="https://capsule-render.vercel.app/api?type=waving&color=0:1a1a2e,50:16213e,100:0f3460&height=200&section=header&text=Global%20Freight%20Performance%20Analytics&fontSize=32&fontColor=ffffff&animation=fadeIn&fontAlignY=38&desc=Route%20Optimization%20%7C%20Cost%20Reduction%20%7C%20Customer%20Retention&descAlignY=58&descSize=16"/>

<br/>

<img src="https://img.shields.io/badge/MySQL-8.0-4479A1?style=for-the-badge&logo=mysql&logoColor=white"/>
<img src="https://img.shields.io/badge/Tableau-Public-E97627?style=for-the-badge&logo=tableau&logoColor=white"/>
<img src="https://img.shields.io/badge/GitHub-Portfolio-181717?style=for-the-badge&logo=github&logoColor=white"/>
<img src="https://img.shields.io/badge/Status-Active-00C853?style=for-the-badge"/>

<br/><br/>

<img src="https://img.shields.io/badge/7%20Tables-Relational%20Schema-4479A1?style=flat-square"/>
<img src="https://img.shields.io/badge/7%2C590%20Rows-Dataset-FF6B35?style=flat-square"/>
<img src="https://img.shields.io/badge/13%20SQL%20Queries-L1%20→%20L3-00C853?style=flat-square"/>
<img src="https://img.shields.io/badge/3PL%20Domain-CEVA%20Logistics-E97627?style=flat-square"/>

<br/><br/>

> **"Data without domain knowledge is just numbers. This project combines 8+ years of freight forwarding expertise with end-to-end analytics to solve real 3PL problems."**
>
> *— Jaspreet Singh, CEVA Logistics*

</div>

---

## 🎯 Executive Summary

This is not a textbook analytics exercise. Every business question, every table design and every SQL query in this project is rooted in real operational challenges I encounter daily as an Ocean Import Coordinator at CEVA Logistics in the Greater Toronto Area.

**The core problem:** Most 3PL teams make carrier and routing decisions based on habit, not data. The result is customers paying more than they should, receiving shipments later than planned and quietly moving their business elsewhere.

**What this project delivers:**

```
❌ BEFORE                          ✅ AFTER
─────────────────────────────────────────────────────
Routing based on habit         →   Data-driven route selection
Carrier chosen by availability →   Carrier scored on cost + speed + OTD
No visibility on churn risk    →   At-risk customers ranked by spend
Reactive peak cost management  →   Seasonal patterns identified early
No negotiation data            →   Volume vs rate benchmarks per lane
Transshipment delays untracked →   Bottleneck days broken into components
```

---

## 🧩 The Four Problems We Solve

<table>
<tr>
<td width="25%" align="center">

### 💰 High Freight Cost
Customers overpaying due to wrong carrier selection, unnecessary peak surcharges and unoptimized routing

</td>
<td width="25%" align="center">

### 🐢 Slow Transit
Transshipment routes adding 4–12 unnecessary days per shipment when direct options exist

</td>
<td width="25%" align="center">

### 📉 Customer Churn
Late deliveries directly correlate with churn probability — but nobody was tracking the connection

</td>
<td width="25%" align="center">

### 📋 No Contract Coverage
Customers without filed contracts face last-minute booking failures and premium spot rates

</td>
</tr>
</table>

---

## 💡 Solutions Built Into This Analysis

| # | Problem | Solution Delivered | Metric |
|---|---|---|---|
| 1 | Carrier selection is gut-feel | Carrier scorecard — cost × speed × reliability | Cost per container by carrier |
| 2 | Transshipment routes not benchmarked | Direct vs transshipment comparison per lane | Days and cost saved |
| 3 | No visibility on routing waste | Route optimization table — before vs after | Annual saving per lane |
| 4 | Customer churn not linked to operations | Delay days mapped to churn probability | Spend at risk by customer |
| 5 | Peak costs spike unpredictably | Monthly cost trend with seasonal patterns | Surcharge by month |
| 6 | Carrier negotiations lack data | Volume vs rate benchmarking per carrier | Leverage points identified |
| 7 | Contract gaps create booking risk | Contract filed status per customer | Customers without coverage |

---

## 🗄️ Database Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                    freight_performance_db                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   carriers (10)          routes_fixed (60)                      │
│       │                       │                                 │
│       └──────────────────┐    │                                 │
│                          ▼    ▼                                 │
│                    shipments_p3 (2,000)                         │
│                    ┌──────┴──────┐                              │
│                    ▼             ▼                              │
│            freight_costs    transit_performance                 │
│              (2,000)            (2,000)                         │
│                    ▼                                            │
│             customers (50)                                      │
│                                                                 │
│   route_optimization_fixed (30) ← The Solution Table            │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

| Table | Rows | What It Measures |
|---|---|---|
| `carriers` | 10 | Contract rates, OTD scores, free days, negotiation status |
| `routes_fixed` | 60 | Direct vs transshipment routes, congestion, transit benchmarks |
| `customers` | 50 | Segment, churn risk, NPS, contract status, last complaint |
| `shipments_p3` | 2,000 | Every shipment — route type, carrier, delay, on-time flag |
| `freight_costs` | 2,000 | Full landed cost breakdown including transshipment fees |
| `transit_performance` | 2,000 | Sailing days, port wait, customs, transshipment wait separately |
| `route_optimization_fixed` | 30 | Before vs after — days saved, cost saved, satisfaction lift |

---

## 📊 Business Questions & SQL Approach

### 🔵 Level 1 — Route & Carrier Performance

| Query | Business Question | Key Insight Delivered |
|---|---|---|
| Q1 | Direct vs transshipment — what is the real cost and time difference? | Quantifies the hidden cost of bad routing |
| Q2 | Which carrier scores best on cost + speed + reliability combined? | Replaces gut-feel carrier selection with data |
| Q3 | Which routes have the most transshipments and worst delays? | Prioritizes optimization efforts |
| Q4 | Where exactly does the extra money go on transshipment routes? | Line-by-line cost breakdown |

### 🟡 Level 2 — Customer Impact Analysis

| Query | Business Question | Key Insight Delivered |
|---|---|---|
| Q5 | Which customers are at churn risk due to poor delivery? | Links operations to revenue risk |
| Q6 | How much annual spend is at risk due to delays? | Attaches a dollar value to service failures |
| Q7 | Which carriers are underperforming vs the network average? | Data for carrier performance conversations |
| Q8 | How is total freight spend trending month over month? | Seasonal pattern for proactive planning |

### 🔴 Level 3 — Optimization & Window Functions

| Query | Business Question | Key Insight Delivered |
|---|---|---|
| Q9 | What did route optimization actually deliver? | Before vs after with real numbers |
| Q10 | Who is the cheapest reliable carrier on each specific trade lane? | Lane-level carrier recommendation |
| Q11 | Which carriers have the best transit efficiency score? | Identifies consistently reliable operators |
| Q12 | What is the full risk scorecard for every customer? | One view — all risk factors combined |
| Q13 | What is the total projected annual saving from all optimized routes? | Business case for continued optimization |

---

## 🧠 SQL Concepts Demonstrated

```sql
/* Level 1 — Multi-Table JOINs */
JOIN carriers c ON s.Carrier_ID = c.Carrier_ID
JOIN freight_costs f ON s.Shipment_ID = f.Shipment_ID

/* Level 2 — Nested CTEs */
WITH Shipment_Summary AS (...),
     Cost_Summary AS (...)
SELECT ... FROM customers c
JOIN Shipment_Summary ss ON c.Customer_ID = ss.Customer_ID

/* Level 3 — Window Functions */
RANK() OVER (PARTITION BY Origin_Port, Destination_Port
             ORDER BY AVG(Cost_Per_Container_USD) ASC)

SUM(SUM(Total_Landed_Cost_USD))
    OVER (ORDER BY Cost_Year, Cost_Month) AS Running_Total
```

---

## 📁 Repository Structure

```
freight-performance-analytics/
│
├── 📂 data/
│   ├── carriers.csv                   # 10 carrier profiles with contract data
│   ├── routes_fixed.csv               # 60 routes — direct and transshipment
│   ├── customers.csv                  # 50 customers with churn risk scores
│   ├── shipments_p3.csv               # 2,000 shipments across all lanes
│   ├── freight_costs.csv              # 2,000 full landed cost breakdowns
│   ├── transit_performance.csv        # 2,000 transit component breakdowns
│   └── route_optimization_fixed.csv   # 30 optimized lanes — before vs after
│
├── 📂 queries/
│   └── freight_performance_analysis.sql   # All 13 SQL queries L1 → L3
│
└── README.md
```

---

## 🗺️ Project Roadmap

- [x] Define business problems from real 3PL operations
- [x] Design 7-table relational schema
- [x] Generate 7,590 rows of interconnected freight data
- [x] Build route optimization table — before vs after
- [x] Load all tables into MySQL
- [x] Write Level 1 queries — route and carrier performance
- [x] Write Level 2 queries — customer impact and churn risk
- [x] Write Level 3 queries — window functions and optimization
- [ ] Build Tableau dashboard — 3 pages
- [ ] Write case study

---

## 👤 About the Author

<table>
<tr>
<td width="70%">

**Jaspreet Singh**
CEVA Logistics | Greater Toronto Area

8+ years across ocean import, air freight, carrier negotiations, D&D cost recovery, pharma cold chain and key account operations.

**Core expertise:** Transpacific & Transatlantic lanes · FCL/LCL operations · CargoWise · Carrier SLA management · Pharma cold chain · CIFFA & FIATA certified

*This project is built on real problems I solve daily — translated into data that any supply chain team can act on.*

</td>
<td width="30%" align="center">

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/jaspreet-singh-5b13b510b/)

[![GitHub](https://img.shields.io/badge/GitHub-Portfolio-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Jaspreet-analyst)

[![Tableau](https://img.shields.io/badge/Tableau-Dashboards-E97627?style=for-the-badge&logo=tableau&logoColor=white)](https://public.tableau.com/app/profile/jaspreet.singh5400/vizzes)

</td>
</tr>
</table>

---

<div align="center">

<img width="100%" src="https://capsule-render.vercel.app/api?type=waving&color=0:0f3460,50:16213e,100:1a1a2e&height=100&section=footer"/>

</div>

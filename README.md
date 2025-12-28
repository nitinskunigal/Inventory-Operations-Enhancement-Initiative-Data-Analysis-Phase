# Inventory Operations Enhancement - Data Analysis Phase (Feeds the Business Analysis Phase)



## 1. Project Context – How This Analysis Fits Into the BA Engagement

This repository contains the **Data Analysis phase** of a broader **Business Analysis (BA) initiative** focused on enhancing inventory execution and control for MapleDash Grocers, a simulated mid-sized e-grocery retailer operating five fulfillment centers (warehouses) across the Greater Toronto Area.

This analysis represents the **Discovery / Current-State Assessment** input into the BA engagement. Its purpose is not to propose solutions, design systems, or define requirements, but to **quantitatively diagnose operational conditions** that require further investigation, validation, and structured problem-solving during the BA phase.

**Key positioning:**
- This is **not** a standalone analytics project  
- Power BI dashboards are **diagnostic tools**, not deliverables in themselves  
- Insights from this analysis directly informed **Gap Analysis, Business Case, BRD, and KPI success criteria**

This phase answers:  
**“What is happening and where are the risks?”**  
not  
**“What should the proposed solution be?”**

---

## 2. How This Analysis Feeds the Business Analysis Phase

This data analysis directly enabled the Business Analysis initiative in the following ways:

- **Gap Analysis:** Inventory imbalance, replenishment risk, and execution gaps quantified here formed the baseline gaps  
- **Process Mapping (AS-IS / TO-BE):** Execution bottlenecks identified here informed process redesign focus areas  
- **Business Case:** KPIs from this analysis became benefits realization metrics (e.g., ATP overselling, coverage efficiency)  
- **BRD Objectives:** Inventory accuracy, replenishment effectiveness, and reduced supervisor dependency were grounded in data  
- **User Stories & UAT Scenarios:** High-risk execution points identified here became system validation checkpoints  

🔗 **Business Analysis GitHub Repository:** *(insert link)*

---

## 3. Objective of This Data Analysis Phase

The objective of this data analysis phase is to establish a **fact-based current-state evidence baseline** that supports downstream Business Analysis activities.

This phase is accountable for:

- Quantifying inventory health, availability, and expiry exposure using consistent KPIs  
- Highlighting execution risks arising from demand volatility and replenishment behavior  
- Identifying warehouse-level throughput and workload imbalance across the network  
- Providing supplier reliability metrics as **contextual inbound risk indicators**, not solution levers  
- Supplying validated, data-backed inputs for gap analysis, root cause exploration, and business case development  

This analysis focuses on **what is happening and where risks exist**, not on prescribing solutions or defining future-state designs.

---

## 4. Data Sources

All datasets used in this analysis were sourced from **historical operational extracts** made available for analytical assessment.

**Data Sources:**
- **Inventory Management System (IMS):** Inventory snapshots  
- **Order Management System (OMS):** Customer orders, order quantities, revenue  
- **Supplier Performance Records:** Historical inbound delivery dates, lead times  

**Important clarifications:**
- These systems are **data sources**, not subjects of redesign here  
- Supplier data reflects **observed inbound performance**, not live integrations  
- Lead time and OTD are **contextual metrics**, not controlled variables  

**Technical approach:**
- CSV files used as primary data sources  
- No SQL extraction required  
- Power BI was used as an analytical tool for this assessment to analyze CSV extracts exported from MapleDash’s operational systems, reflecting MapleDash’s current analytical maturity.
- Automated pipelines and database-driven reporting are planned as part of future BA-led initiatives but were not in scope for this assessment.  

---

## 5. Insights & Root Causes

Root causes listed below are **data-indicated hypotheses** derived from observed patterns. Formal validation and solution design occur during the Business Analysis phase.

### 5.1 Executive Inventory Snapshot – Category-Level Context

![5.1](https://github.com/nitinskunigal/Inventory-Operations-Enhancement-Initiative-Data-Analysis-Phase/blob/main/DA%20Deliverables/Screenshots%20of%20Visuals%20for%20Insights/5.1%20Executive%20Inventory%20Snapshot%20%E2%80%93%20Systemic%20Inventory%20Health.png)

**Business Questions Answered**
- Which categories drive inventory value?
- Which categories depress turnover?
- Is poor turnover systemic or category-specific?

**Insights**
- Over 60% of inventory value is tied to long-expiry stock  
- Slow-moving categories hold disproportionate inventory value and exhibit very low turnover, inflating Days of Inventory
- Perishables move faster but operate with tighter buffers.  

**Implication**
- Aggregate KPIs mask category-level inefficiencies  

**Data-Indicated Root Causes**
- MOQ (Minimum Order Quantity)-driven procurement
- Uniform replenishment logic across fundamentally different categories
- Weak coupling between demand velocity and stocking behavior.

---

### 5.2 Demand Volatility, Revenue Concentration & SKU Risk (ABC–XYZ)

#### 5.2.1 SKU Portfolio Structure & Revenue Exposure (ABC)

![5.2.1 ABC Pareto Chart](https://github.com/nitinskunigal/Inventory-Operations-Enhancement-Initiative-Data-Analysis-Phase/blob/main/DA%20Deliverables/Screenshots%20of%20Visuals%20for%20Insights/5.2%20Demand%20Volatility%2C%20Revenue%20Concentration%20%26%20SKU%20Risk%20(ABC%E2%80%93XYZ)/5.2.1%20Distribution%20of%20SKUs%20%26%20Revenue%20Share%20Across%20ABC.png) 
![5.2.1 Revenue by ABC & Category Mix](https://github.com/nitinskunigal/Inventory-Operations-Enhancement-Initiative-Data-Analysis-Phase/blob/main/DA%20Deliverables/Screenshots%20of%20Visuals%20for%20Insights/5.2%20Demand%20Volatility%2C%20Revenue%20Concentration%20%26%20SKU%20Risk%20(ABC%E2%80%93XYZ)/5.2.1%20Revenue%20by%20ABC%20%26%20Category%20Mix.png)

**Business Questions Answered**
- How concentrated is revenue across the SKU portfolio?
- How many SKUs are revenue-critical?
- Which categories dominate A-class revenue?

**Insights**
- A-class contains the largest share of SKUs
- These SKUs collectively drive most revenue
- Revenue concentration exists across multiple categories

**Implication**
- Execution reliability is required across a broad SKU base
- •	Errors in inventory accuracy affect many SKUs, not just a few.

**Data-Indicated Root Causes**
- SKU assortment expanded without execution-tier differentiation.
- No operational prioritization for revenue-critical SKUs.
- Inventory policies treat high- and low-impact SKUs similarly.

---

#### 5.2.2 Combined ABC–XYZ Risk Profile

![5.2.2](https://github.com/nitinskunigal/Inventory-Operations-Enhancement-Initiative-Data-Analysis-Phase/blob/main/DA%20Deliverables/Screenshots%20of%20Visuals%20for%20Insights/5.2%20Demand%20Volatility%2C%20Revenue%20Concentration%20%26%20SKU%20Risk%20(ABC%E2%80%93XYZ)/5.2.2%20Revenue%20%26%20Order%20Distribution%20Across%20ABC%E2%80%93XYZ.png)

**Business Questions Answered**
- Which SKUs are both high-value and volatile?
- Where is execution risk concentrated?

**Insights**
- A/Y and A/Z SKUs dominate revenue and workload
- High volatility + high value creates execution risk (stockouts and overselling)
- C/X empty → low-value products rarely have stable demand, typical for e-grocery.

**Implication**
- These SKUs must be protected by system-driven controls.  

**Data-Indicated Root Causes**
- ABC–XYZ classification not operationalized
- No differentiated safeguards for high-risk SKUs.

---

#### 5.2.3 Demand Volatility & Workload Instability (XYZ)

![5.2.3](https://github.com/nitinskunigal/Inventory-Operations-Enhancement-Initiative-Data-Analysis-Phase/blob/main/DA%20Deliverables/Screenshots%20of%20Visuals%20for%20Insights/5.2%20Demand%20Volatility%2C%20Revenue%20Concentration%20%26%20SKU%20Risk%20(ABC%E2%80%93XYZ)/5.2.3%20Monthly%20Distribution%20of%20Orders%20%26%20Revenue%20Across%20XYZ.png)

**Business Questions Answered**
- How volatile is demand?
- How predictable is daily operational workload?

**Insights**
- Y-class dominates order volume, indicating sustained volatility.
- Z-class causes promotion-driven spikes  

**Implication**
- Static execution rules fail under volatility
- Manual interventions increase under volatile demand.

**Data-Indicated Root Cause**
- Replenishment cadence not aligned with volatility.

---

### 5.3 Inventory Distribution, Velocity & Execution Risk

#### 5.3.1 Demand Velocity vs Inventory Coverage

![5.3.1](https://github.com/nitinskunigal/Inventory-Operations-Enhancement-Initiative-Data-Analysis-Phase/blob/main/DA%20Deliverables/Screenshots%20of%20Visuals%20for%20Insights/5.3%20Inventory%20Distribution%2C%20Velocity%20%26%20Execution%20Risk/5.3.1%20Demand%20Velocity%20vs%20Inventory%20Coverage.png)

**Business Questions Answered**
- Is inventory aligned with actual consumption?
- Where are stockouts likely despite healthy totals?

**Insights**
- Fast-moving categories have lower coverage.
- Slow movers carry excess stock.

**Implication**
- Stockouts coexist with overstocking
- Replenishment is misaligned with demand reality.

**Data-Indicated Root Causes**
- Purchase quantities driven by supplier constraints.
- Poor backstock-to-pick-zone translation.

---

#### 5.3.2 FIFO vs FEFO Execution Discipline

![5.3.2](https://github.com/nitinskunigal/Inventory-Operations-Enhancement-Initiative-Data-Analysis-Phase/blob/main/DA%20Deliverables/Screenshots%20of%20Visuals%20for%20Insights/5.3%20Inventory%20Distribution%2C%20Velocity%20%26%20Execution%20Risk/5.3.2%20FIFO%20vs%20FEFO%20Execution%20Discipline.png)

**Business Questions Answered**
- Is expiry risk operationally managed?
- Are perishable SKUs rotated correctly?

**Insights**
- Short shelf-life categories show FEFO leakage.
- Expiry risk is execution-driven, not demand-driven.

**Implication**
- Spoilage risk is execution-driven  

**Data-Indicated Root Cause**
- FEFO not enforced operationally

---

### 5.4 Warehouse Throughput & Network Imbalance

![5.4](https://github.com/nitinskunigal/Inventory-Operations-Enhancement-Initiative-Data-Analysis-Phase/blob/main/DA%20Deliverables/Screenshots%20of%20Visuals%20for%20Insights/5.4%20Warehouse%20Throughput%20%26%20Network%20Imbalance.png)

**Business Question Answered**
- Is operational workload evenly distributed across the fulfillment network?

**Insights**
- Three FCs contribute over 70% of revenue and order volume, while others remain underutilized.
- Category mix varies significantly by FC, creating uneven operational load.

**Implication**
- Congested FCs amplify the impact of inbound delays and inventory inaccuracies.  

**Data-Indicated Root Causes**
- Inventory allocation does not align with geographic demand.
- Inbound scheduling and replenishment rules are FC-agnostic.
- No systematic balancing mechanism across warehouses.

---

### 5.5 Supplier Reliability & Inbound Risk Exposure

Supplier metrics provide **risk context**, not solution levers.

#### 5.5.1 Supplier Performance Matrix (Reliability vs Lead Time)

![5.5.1](https://github.com/nitinskunigal/Inventory-Operations-Enhancement-Initiative-Data-Analysis-Phase/blob/main/DA%20Deliverables/Screenshots%20of%20Visuals%20for%20Insights/5.5%20Supplier%20Reliability%20%26%20Inbound%20Risk%20Exposure/5.5.1%20Supplier%20Performance%20Matrix%20(Reliability%20vs%20Lead%20Time).png)

**Business Question Answered**
- How predictable is inbound supply into the warehouses?

**Insights**
- Overall supplier OTD averages 66.7%, well below grocery benchmarks.
- Many suppliers exhibit both low reliability and long lead times.

**Implication**
- Inbound predictability is low
- Inventory planning based on expected receipts is fragile.
- Execution controls must absorb variability.

**Data-Indicated Root Causes**
- No reliability-based supplier segmentation
- Inbound processes assume plan adherence rather than execution variability.
- Limited feedback loop from operations to procurement.

---

#### 5.5.2 Supplier Cost vs Reliability Tradeoff

![5.5.2](https://github.com/nitinskunigal/Inventory-Operations-Enhancement-Initiative-Data-Analysis-Phase/blob/main/DA%20Deliverables/Screenshots%20of%20Visuals%20for%20Insights/5.5%20Supplier%20Reliability%20%26%20Inbound%20Risk%20Exposure/5.5.2%20Supplier%20Cost%20vs%20Reliability%20Tradeoff.png)

**Business Question Answered**
- How much variability exists in replenishment lead times?

**Insights**
- Several higher-cost suppliers deliver unreliably.
- Some lower-cost suppliers perform better but are underutilized.
- No dominant “low-cost, high-reliability” supplier group exists.

**Implication**
- Operational inefficiency offsets unit-cost savings

**Data-Indicated Root Causes**
- Supplier evaluation lacks multi-dimensional scoring.
- Reliability is not weighted sufficiently in purchasing decisions.
- Inventory buffers compensate for supplier issues instead of addressing them.

---

#### 5.5.3 Supplier Concentration Risk

![5.5.3](https://github.com/nitinskunigal/Inventory-Operations-Enhancement-Initiative-Data-Analysis-Phase/blob/main/DA%20Deliverables/Screenshots%20of%20Visuals%20for%20Insights/5.5%20Supplier%20Reliability%20%26%20Inbound%20Risk%20Exposure/5.5.3%20Supplier%20Concentration%20Risk.png)

**Business Question Answered**
- How exposed is MapleDash to supplier dependency risk?

**Insights**
- Top 3 suppliers account for 28% of total ATP, nearing concentration risk thresholds.

**Implication**
- Disruption from a single supplier can cascade across multiple FCs.
- System resilience becomes critical.

**Data-Indicated Root Causes**
- Limited dual sourcing for critical SKUs.
- No supplier criticality classification.
- Inventory policies do not adjust for dependency risk.

---

### 5.6 Sales Pressure & Operational Load Context

![5.6](https://github.com/nitinskunigal/Inventory-Operations-Enhancement-Initiative-Data-Analysis-Phase/blob/main/DA%20Deliverables/Screenshots%20of%20Visuals%20for%20Insights/5.6%20Sales%20Pressure%20%26%20Operational%20Load%20Context.png)

**Business Question Answered**
- Are operational issues demand-driven or execution-driven?

**Insights**
- Demand peaks mid-year with clear seasonal spikes.
- Promotions drive volatility rather than steady baseline demand.

**Implication**
- Inventory and replenishment systems must react to execution timing, not forecasts alone.
- Manual controls struggle during peak periods.  

**Data-Indicated Root Causes**
- Replenishment logic is not seasonality-aware.
- Inventory updates lag during peak operational load.
- Process design assumes stable demand patterns that do not exist.

---

### 5.7 Closing Insight

Collectively, these insights show that MapleDash’s challenges stem from:
- Execution timing gaps
- SKU-level imbalance hidden by aggregates
- Supplier variability that must be absorbed operationally
- Overreliance on manual intervention

---

## 6. Why Recommendations Are Not Included Here

This repository intentionally stops at **diagnosis**, not design.

Formal RCA and recommendations require:
- Stakeholder interviews
- Process walkthroughs
- Feasibility and cost–benefit analysis  

These occur in the **Business Analysis phase**, where this analysis serves as validated current-state input.

---

## 7. Key Deliverables & Links

- Interactive Power BI Dashboard  
- **[Screenshots of Power BI Report Pages](https://github.com/nitinskunigal/Inventory-Operations-Enhancement-Initiative-Data-Analysis-Phase/tree/main/DA%20Deliverables/Screenshots%20of%20Power%20BI%20Report%20Pages)**  
- **[KPI Dictionary](https://github.com/nitinskunigal/Inventory-Operations-Enhancement-Initiative-Data-Analysis-Phase/blob/main/DA%20Deliverables/KPI%20Dictionary.pdf)**
- **[Data Dictionary](https://github.com/nitinskunigal/Inventory-Operations-Enhancement-Initiative-Data-Analysis-Phase/blob/main/DA%20Deliverables/Data%20Dictionary.pdf)**
- **[Business Analysis Project Repository](https://github.com/nitinskunigal/Inventory-Operations-Enhancement-Initiative-Business-Analysis-Phase)**

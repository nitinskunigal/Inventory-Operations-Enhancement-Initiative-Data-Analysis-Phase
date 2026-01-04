# Inventory Operations Enhancement - Data Analysis Phase (Feeds the Business Analysis Initiative)

## Table of Contents

- [1. Project Context](#1-project-context)
- [2. How This Analysis Feeds the Business Analysis Phase](#2-how-this-analysis-feeds-the-business-analysis-phase)
- [3. Objective of This Data Analysis Phase](#3-objective-of-this-data-analysis-phase)
- [4. Data Sources](#4-data-sources)
- [5. Insights and Root Causes](#5-insights-and-root-causes)
- [6. Why Recommendations Are Not Included Here](#6-why-recommendations-are-not-included-here)
- [7. Key Deliverables and Links](#7-key-deliverables-and-links)

## 1. Project Context

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

🔗 **[Business Analysis GitHub Repository](https://github.com/nitinskunigal/Inventory-Operations-Enhancement-Initiative-Business-Analysis-Phase)**

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
- Power BI was used as an analytical tool for this assessment to analyze CSV extracts exported from MapleDash’s operational systems, reflecting MapleDash’s current analytical maturity.
- Automated pipelines and database-driven reporting are planned as part of future BA-led initiatives but were not in scope for this assessment.

---

## 5. Insights and Root Causes

This section translates dashboard visuals into operational understanding. Rather than listing KPIs or isolated observations, the insights below explain what is happening, why it matters operationally, and where risk is accumulating across inventory, demand, warehouse execution, and inbound supply. All insights are derived from observed patterns in the data. Root causes are data-indicated hypotheses, not finalized conclusions. In real Business Analysis practice, these hypotheses are validated later through stakeholder interviews, process walkthroughs, and feasibility assessment. The purpose here is diagnosis, not solution design.

### 5.1 Executive Inventory Snapshot – Category-Level Context

<p align="center">
  Inventory value is concentrated in slow-moving categories, suppressing overall turnover while masking stockout risk in faster-moving categories
</p>
<p align="center">
  <img src=https://github.com/nitinskunigal/Inventory-Operations-Enhancement-Data-Driven-Current-State-Analysis/blob/main/DA%20Deliverables/Screenshots%20of%20Visuals%20for%20Insights/5.1%20Executive%20Inventory%20Snapshot%20%E2%80%93%20Systemic%20Inventory%20Health.png alt=5.1 width="1000"/>
</p>

**Insights**

At an aggregate level, MapleDash’s inventory appears heavily capitalized, with approximately $1.6M in total inventory value. However, a category-level view reveals that more than 60% of this value is tied up in long-expiry inventory exceeding 90 days. This concentration is not evenly distributed across categories.

Slow-moving categories such as Beverages, Pantry, Household, and Personal Care hold a disproportionate share of inventory value while exhibiting very low turnover. In contrast, perishable and high-velocity categories move inventory faster but operate with much tighter buffers. As a result, overall inventory KPIs present a misleading picture: weak turnover appears systemic, while the real risk is unevenly distributed between overstocked slow movers and under-buffered fast movers.

Operationally, this imbalance creates a dual problem. Working capital is locked in categories with limited demand velocity, while categories that drive fulfillment volume are more exposed to execution delays and stockouts. This explains why fulfillment issues can occur even when total inventory levels appear sufficient.

**Data-Indicated Root Causes**
- Replenishment logic appears category-agnostic, applying similar rules across products with vastly different shelf lives.
- Procurement behavior is likely influenced by minimum order quantities and cost incentives, encouraging bulk purchases in slow-moving categories.
- Weak alignment between demand velocity and stocking behavior, particularly for ambient, long-shelf-life items.

---

### 5.2 Demand Volatility, Revenue Concentration & SKU Risk (ABC–XYZ)

#### 5.2.1 SKU Portfolio Structure & Revenue Exposure (ABC)

<p align="center"> Revenue-critical SKUs are not a narrow subset, expanding execution risk across a large portion of the assortment</p>
<p align="center">
  <img src=https://github.com/nitinskunigal/Inventory-Operations-Enhancement-Data-Driven-Current-State-Analysis/blob/main/DA%20Deliverables/Screenshots%20of%20Visuals%20for%20Insights/5.2%20Demand%20Volatility%2C%20Revenue%20Concentration%20%26%20SKU%20Risk%20(ABC%E2%80%93XYZ)/5.2.1%20Distribution%20of%20SKUs%20%26%20Revenue%20Share%20Across%20ABC.png alt=5.2.1 ABC Pareto Chart width="600"/>
</p>
<p align="center">
  <img src=https://github.com/nitinskunigal/Inventory-Operations-Enhancement-Data-Driven-Current-State-Analysis/blob/main/DA%20Deliverables/Screenshots%20of%20Visuals%20for%20Insights/5.2%20Demand%20Volatility%2C%20Revenue%20Concentration%20%26%20SKU%20Risk%20(ABC%E2%80%93XYZ)/5.2.1%20Revenue%20by%20ABC%20%26%20Category%20Mix.png alt=5.2.1 Revenue by ABC & Category Mix width="600"/>
</p>

**Insights**

Unlike a classic Pareto distribution, MapleDash’s A-class SKUs are not limited to a small, tightly controlled group. Instead, A-class represents a large share of the overall SKU base while collectively driving the majority of revenue. This means that execution reliability is required across many SKUs, not just a handful of top sellers.

Revenue concentration within A-class SKUs is particularly strong in categories such as Frozen, Meat, Seafood, and Personal Care. These categories are both operationally intensive and customer-critical, amplifying the impact of inventory inaccuracies, delayed replenishment, or picking disruptions. Any execution failure in these SKUs disproportionately affects sales performance and customer experience.

**Data-Indicated Root Causes**
- SKU assortment expanded without tiered execution controls based on revenue impact.
- No operational prioritization differentiating revenue-critical SKUs from low-impact items.
- Uniform inventory policies applied across SKUs with very different business criticality.

---

#### 5.2.2 Combined ABC–XYZ Risk Profile - Strategic SKU Misalignment

<p align="center"> High-value, volatile SKUs dominate both revenue and workload, concentrating execution risk where failures hurt most </p>
<p align="center">
  <img src=https://github.com/nitinskunigal/Inventory-Operations-Enhancement-Data-Driven-Current-State-Analysis/blob/main/DA%20Deliverables/Screenshots%20of%20Visuals%20for%20Insights/5.2%20Demand%20Volatility%2C%20Revenue%20Concentration%20%26%20SKU%20Risk%20(ABC%E2%80%93XYZ)/5.2.2%20Revenue%20%26%20Order%20Distribution%20Across%20ABC%E2%80%93XYZ.png alt=5.2.2 width="600"/>
</p>

**Insights**

When SKU value (ABC) is combined with demand volatility (XYZ), execution risk becomes highly concentrated. A/Y and A/Z SKUs dominate both revenue contribution and operational workload. These SKUs are simultaneously high-value and unpredictable, making them the most exposed to overselling, stockouts, and replenishment failures.

The absence of C/X SKUs, which would represent low-value, stable demand items, is typical for e-grocery and confirms that stable, low-risk demand is rare. As a result, MapleDash operates in an environment where most operational effort is concentrated on SKUs that require tight execution discipline. Manual controls and uniform rules struggle to scale under this level of volatility.

**Data-Indicated Root Causes**
- ABC–XYZ classification exists analytically but is not operationalized.
- High-risk SKUs lack differentiated safeguards or priority handling.
- Execution controls rely on manual intervention rather than system-directed rules.

---

#### 5.2.3 Demand Volatility & Workload Instability (XYZ)

<p align="center"> Sustained demand volatility undermines static replenishment and cycle counting practices </p>
<p align="center">
  <img src=https://github.com/nitinskunigal/Inventory-Operations-Enhancement-Data-Driven-Current-State-Analysis/blob/main/DA%20Deliverables/Screenshots%20of%20Visuals%20for%20Insights/5.2%20Demand%20Volatility%2C%20Revenue%20Concentration%20%26%20SKU%20Risk%20(ABC%E2%80%93XYZ)/5.2.3%20Distribution%20of%20Orders%20Across%20XYZ.png alt=5.2.3 width="1000"/>
</p>

**Insights**

Y-class demand dominates order volume, indicating persistent variability rather than isolated spikes. Z-class demand introduces periodic surges, often tied to promotions, further destabilizing workload patterns. This volatility directly affects replenishment timing, picking efficiency, and cycle count effectiveness.

In an environment where demand is neither stable nor predictable, static replenishment cadences and manual cycle count planning become increasingly ineffective. Operational teams are forced into reactive behavior, increasing supervisor intervention and reducing system trust.

**Data-Indicated Root Cause**
- Replenishment cadence not aligned with demand volatility.
- Cycle counting not risk-weighted based on SKU volatility.
- Execution rules assume stability that does not exist in practice.

---

### 5.3 Inventory Distribution, Velocity & Execution Risk

#### 5.3.1 Demand Velocity vs Inventory Coverage

<p align="center"> Inventory is positioned opposite to consumption patterns, creating simultaneous overstocking and stockouts </p>
<p align="center">
  <img src=https://github.com/nitinskunigal/Inventory-Operations-Enhancement-Data-Driven-Current-State-Analysis/blob/main/DA%20Deliverables/Screenshots%20of%20Visuals%20for%20Insights/5.3%20Inventory%20Distribution%2C%20Velocity%20%26%20Execution%20Risk/5.3.1%20Demand%20Velocity%20vs%20Inventory%20Coverage.png alt=5.3.1 width="800"/>
</p>

**Insights**

Fast-moving categories such as Fresh Produce, Frozen, and Meat operate with lower days of cover, while slow-moving categories carry excess coverage relative to demand. This misalignment creates a paradox where stockouts and overstocking coexist across the network.

Even when total inventory appears sufficient, high-velocity categories run closer to risk due to tighter buffers and execution delays. Meanwhile, excess inventory in slow movers suppresses overall turnover and inflates holding costs. The issue is not total inventory quantity, but where inventory is positioned relative to demand.

**Data-Indicated Root Causes**
- Purchase quantities driven by supplier constraints rather than consumption patterns.
- Weak translation of backstock into pick-face availability.
- Replenishment rules not calibrated to demand velocity.

---

#### 5.3.2 FIFO vs FEFO Execution Discipline

<p align="center"> Expiry risk is driven by execution discipline gaps, not forecasting or demand </p>
<p align="center">
  <img src=https://github.com/nitinskunigal/Inventory-Operations-Enhancement-Data-Driven-Current-State-Analysis/blob/main/DA%20Deliverables/Screenshots%20of%20Visuals%20for%20Insights/5.3%20Inventory%20Distribution%2C%20Velocity%20%26%20Execution%20Risk/5.3.2%20FIFO%20vs%20FEFO%20Execution%20Discipline.png alt=5.3.2 width="400"/>
</p>

**Insights**

Short shelf-life categories show clear leakage between FIFO and FEFO value, indicating that inventory is not consistently rotated based on expiry. This leakage persists even when headline expiry KPIs appear manageable, suggesting that risk is embedded in day-to-day execution rather than demand forecasting errors.

Operationally, this means spoilage and markdown risk is introduced through handling and placement decisions, not through excessive inventory levels alone. Without enforced FEFO logic at execution points, expiry exposure accumulates silently.

**Data-Indicated Root Cause**
- FEFO not enforced during putaway and picking.
- Expiry attributes not operationalized in execution workflows.
- Manual judgment substituting for system-driven rotation logic.

---

### 5.4 Warehouse Throughput & Network Imbalance

<p align="center"> Execution risk is amplified by uneven workload distribution across fulfillment centers </p>
<p align="center">
  <img src=https://github.com/nitinskunigal/Inventory-Operations-Enhancement-Initiative-Data-Analysis-Phase/blob/main/DA%20Deliverables/Screenshots%20of%20Visuals%20for%20Insights/5.4%20Warehouse%20Throughput%20%26%20Network%20Imbalance.png alt=5.4 width="1000"/>
</p>

**Insights**

Three fulfillment centers account for over 70% of total order volume and revenue, while the remaining facilities operate at significantly lower throughput. Category mix varies sharply by location, with high-volume FCs handling more complex, fast-moving assortments.

This imbalance magnifies the impact of execution gaps. Inbound delays, replenishment failures, or inventory inaccuracies have a non-linear effect in high-throughput locations, where volume leaves little room for recovery. Meanwhile, unused capacity exists elsewhere in the network, but without systematic rebalancing mechanisms.

**Data-Indicated Root Causes**
- Inventory allocation not aligned with geographic demand patterns.
- One-size-fits-all execution rules applied across heterogeneous FCs.
- Limited system awareness of FC-specific demand velocity and volatility.

---

### 5.5 Supplier Reliability & Inbound Risk Exposure

#### 5.5.1 Supplier Performance Matrix (Reliability vs Lead Time)

<p align="center"> Inbound unpredictability requires execution controls that absorb variability, not assume plan adherence </p>
<p align="center">
  <img src=https://github.com/nitinskunigal/Inventory-Operations-Enhancement-Data-Driven-Current-State-Analysis/blob/main/DA%20Deliverables/Screenshots%20of%20Visuals%20for%20Insights/5.5%20Supplier%20Reliability%20%26%20Inbound%20Risk%20Exposure/5.5.1%20Supplier%20Performance%20Matrix%20(Reliability%20vs%20Lead%20Time).png alt=5.5.1 width="500"/>
</p>

**Insights**

Average supplier on-time delivery stands at approximately 66.7%, well below typical grocery benchmarks. Many suppliers combine low reliability with long lead times, creating inherently unpredictable inbound flows. Disruption from a single supplier can cascade across multiple fulfillment centers.

This variability weakens inventory planning assumptions and increases reliance on execution discipline. When inbound receipts cannot be trusted, systems must delay ATP release and enforce validation points to prevent downstream distortion.

**Data-Indicated Root Causes**
- Suppliers not segmented by reliability or criticality.
- Inbound processes assume plan adherence rather than variability.
- Limited operational feedback into procurement decisions.

---

#### 5.5.2 Supplier Cost vs Reliability Tradeoff

<p align="center"> Unit cost optimization masks downstream execution cost and risk </p>
<p align="center">
  <img src=https://github.com/nitinskunigal/Inventory-Operations-Enhancement-Data-Driven-Current-State-Analysis/blob/main/DA%20Deliverables/Screenshots%20of%20Visuals%20for%20Insights/5.5%20Supplier%20Reliability%20%26%20Inbound%20Risk%20Exposure/5.5.2%20Supplier%20Cost%20vs%20Reliability%20Tradeoff.png alt=5.5.2 width="600"/>
</p>

**Insights**

Several higher-cost suppliers still deliver unreliably, while some lower-cost suppliers perform better but are underutilized. No clear “low-cost, high-reliability” supplier group exists, indicating that procurement decisions may not fully account for execution impact.

Operational inefficiencies such as expediting, buffering, and firefighting often offset perceived unit cost savings. Without visibility into this trade-off, cost-focused decisions inadvertently increase operational risk.

**Data-Indicated Root Causes**
- Supplier evaluation lacks multi-dimensional scoring.
- Reliability underweighted relative to unit cost.
- Execution impact of delays not fully quantified.

---

### 5.7 Closing Insight

Collectively, these insights show that MapleDash’s challenges are not driven by missing systems or insufficient data. Instead, risk accumulates through execution timing gaps, SKU-level imbalance hidden by aggregates, uneven workload distribution, and inbound variability that the current operating model cannot absorb.

These patterns explain why manual intervention has become the dominant control mechanism and why performance degrades as scale increases. The findings directly inform the Business Analysis phase, where system-directed execution, automated inventory updates, and exception-based controls are designed to close these gaps.

---

## 6. Why Recommendations Are Not Included Here

This repository intentionally stops at **diagnosis**, not design.

Formal RCA and recommendations require:
- Stakeholder interviews
- Process walkthroughs
- Feasibility and cost–benefit analysis  

These occur in the **Business Analysis phase**, where this analysis serves as validated current-state input.

---

## 7. Key Deliverables and Links

- **[Interactive Power BI Dashboard](https://app.powerbi.com/view?r=eyJrIjoiZmRmNGRhOGEtN2IyNi00ZWNjLTkxN2YtMmYyMzJhNzNhN2NmIiwidCI6ImM2ZTU0OWIzLTVmNDUtNDAzMi1hYWU5LWQ0MjQ0ZGM1YjJjNCJ9)**  
- **[Screenshots of Power BI Report Pages](https://github.com/nitinskunigal/Inventory-Operations-Enhancement-Initiative-Data-Analysis-Phase/tree/main/DA%20Deliverables/Screenshots%20of%20Power%20BI%20Report%20Pages)**  
- **[KPI Dictionary](https://github.com/nitinskunigal/Inventory-Operations-Enhancement-Initiative-Data-Analysis-Phase/blob/main/DA%20Deliverables/KPI%20Dictionary.pdf)**
- **[Data Dictionary](https://github.com/nitinskunigal/Inventory-Operations-Enhancement-Initiative-Data-Analysis-Phase/blob/main/DA%20Deliverables/Data%20Dictionary.pdf)**
- **[Business Analysis Project Repository](https://github.com/nitinskunigal/Inventory-Operations-Enhancement-Initiative-Business-Analysis-Phase)**

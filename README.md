# 📊 Sales-Analytics-Performance-Tracker (Power BI)
*A full end-to-end analytical solution for revenue insights, sales optimization, and strategic decision-making.*

  you can explore the project [here](https://app.powerbi.com/view?r=eyJrIjoiM2FlN2VmNDMtMDc3YS00MDRjLWIzNmQtMzdjZDQwNmJiN2VlIiwidCI6IjU2NDM4N2U5LWNmMTEtNDI3Yy1hNmY3LTcxZGU2MWFlZTQxNyJ9) 

<img width="1060" height="798" alt="Screenshot (103)" src="https://github.com/user-attachments/assets/e32633a8-db5f-4301-af77-cca1f6d8f6eb" />

---

## 📌 **Project Background**

A mid-sized **mechanical equipment supplier** operating across five regions (South, Central, North, West, East) has experienced rapid expansion over the last two years. With a diverse product portfolio **Crane, Excavator, Bulldozer, Loader, and Generator**, the company serves **Individual customers, Distributors, and Corporate clients**.

As sales volume surpassed **10,000 transactions**, leadership faced several challenges:

* Difficulty identifying **top and underperforming sales reps**
* Limited visibility into **regional revenue patterns**
* Misalignment between performance and **sales targets**
* Unclear contribution of key **product categories**
* Need to manage operational strain caused by **50% YoY growth**

To resolve these issues, the executive team requested a **Sales Performance Dashboard** to consolidate analytics, track KPIs, and support data-driven decision-making.

This project delivers a complete Power BI solution that transforms raw data into accessible, actionable business intelligence.

---

## 🎯 **Key Business Questions**

The dashboard addresses the following questions:

* Who are the strongest and weakest sales reps, and how close are they to achieving their targets?
* Which regions and customer types drive the highest revenue?
* What products contribute most to sales volume and profitability?
* How stable is revenue across customer segments and regions?
* What are the major risks and opportunities for growth?

---

Key Insights (Summary)

1️⃣ YoY Growth

The business achieved 50% year-over-year revenue growth, indicating strong market expansion.

2️⃣ Customer Type Contribution

Revenue is evenly distributed across Individual (33%), Distributor (34%), and Corporate (33%).

A balanced portfolio reduces dependency risk.

3️⃣ Regional Revenue

South region leads in total revenue, followed closely by Central, North, West, and East.

No single region dominates → wide, diversified performance.

4️⃣ Product Contribution

High-value products (Crane, Excavator, Bulldozer) lead revenue.

Loader and Generator achieve similar unit volume but lower revenue due to pricing.

5️⃣ Sales Rep Performance Variance

Some high-volume reps underperform against target, while lower-volume reps exceed expectations.

Misalignment indicates flaws in target-setting methodology.

---


## 🧠 **Insights & Recommendations**

| **Metrics**                           | **Insight**                                                                                                                                               | **Recommendation**                                                                                                                                                               |
| ---------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **YoY Revenue Growth**             | The business achieved **50% YoY revenue growth**, signaling rapid market expansion and strong demand.                                                     | **Scale Operations.** Invest in IT systems, logistics, and supply chain capacity to sustain growth while avoiding service delays or bottlenecks.                                 |
| **Customer Type Contribution**     | Revenue is evenly distributed across Individual (33.06%), Distributor (33.67%), and Corporate (33.27%), minimizing dependency risk.                       | **Maintain Balanced Segmentation.** Strengthen retention strategies for each segment and design targeted campaigns to boost average revenue per customer type.                   |
| **Regional Revenue Contribution**  | Revenue is well-distributed, with South leading (1.89B) but Central, North, West, and East close behind. No region dominates → diversified performance.   | **Optimize Regional Strategies.** Identify best-performing tactics in South and replicate them across other regions to increase consistency and unlock additional growth.        |
| **Product Contribution**           | Crane, Excavator, and Bulldozer generate the highest revenue. Loader and Generator have similar unit volume but lower revenue due to pricing differences. | **Optimize Pricing & Stock Levels.** Maintain 99% stock availability for top products. Introduce pricing reviews or bundle strategies to lift revenue from Loader and Generator. |
| **Sales Rep Performance Variance** | Target performance is misaligned: some high-revenue reps are missing targets while lower-revenue reps exceed theirs.                                      | **Recalibrate Targets & Incentives.** Audit target-setting processes and design fair, performance-based KPIs to improve motivation and accuracy.                                 |



## 🧩 **Data Model Overview**

<img width="1185" height="744" alt="Screenshot (106)" src="https://github.com/user-attachments/assets/df2225a5-201f-446f-bae6-8c6b20b90794" />


The project follows a **Star Schema** for optimal performance:

### **Fact Table**

* **FactSales**
  Contains revenue, units sold, discounts, targets, dates, and foreign keys.

### **Dimension Tables**

* **DimDate**
* **DimProduct**
* **DimRegion**
* **DimCustomerType**
* **DimSalesRep**

This model supports flexible slicing (dimensions) and metric calculations (facts).

---
## 📊 Key Metrics

| **Metric**                    | **Definition**                                                      | **Calculation (Conceptual)**                                        |
| ----------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| **Total Revenue**             | Total sales value generated across all transactions.                | `SUM(FactSales[SalesAmount])`                                       |
| **Total Units Sold**          | Total number of product units sold.                                 | `SUM(FactSales[Quantity])`                                          |
| **Total Transactions**        | Count of all sales transactions.                                    | `COUNTROWS(FactSales)`                                              |
| **Average Deal Size**         | Average revenue per transaction.                                    | `Total Revenue / Total Transactions`                                |
| **Avg Revenue per Sales Rep** | Average revenue generated per Sales Representative.                 | `AVERAGEX(VALUES(DimSalesRep[SalesRep]), [Total Revenue])`          |
| **Revenue per Sales Rep**     | Sales revenue generated by each Sales Representative.               | `CALCULATE([Total Revenue], VALUES(DimSalesRep[SalesRep]))`         |
| **Sales Rep Variance**        | Deviation of each rep’s revenue from the average.                   | `[Total Revenue] - [Avg Revenue per Sales Rep]`                     |
| **Top Product Revenue**       | Revenue generated by the highest-performing product categories.     | `TOPN / CALCULATE([Total Revenue], Product Category Filter)`        |
| **Revenue per Customer Type** | Revenue contribution from each customer segment.                    | `CALCULATE([Total Revenue], VALUES(DimCustomerType[CustomerType]))` |
| **Customer Type %**           | Percentage of total revenue attributed to each customer segment.    | `[Revenue per Customer Type] / [Total Revenue]`                     |
| **Revenue LY**                | Revenue from the previous year.                                     | `CALCULATE([Total Revenue], DATEADD(DimDate[Date], -1, YEAR))`      |
| **YoY Revenue Growth %**      | Percentage growth compared to last year.                            | `([Total Revenue] - [Revenue LY]) / [Revenue LY]`                   |
| **YTD Revenue**               | Revenue accumulated from the start of the year to the current date. | `TOTALYTD([Total Revenue], DimDate[Date])`                          |
| **MTD Revenue**               | Revenue accumulated from the start of the month to date.            | `TOTALMTD([Total Revenue], DimDate[Date])`                          |
| **QTD Revenue**               | Revenue accumulated from the start of the quarter to date.          | `TOTALQTD([Total Revenue], DimDate[Date])`                          |



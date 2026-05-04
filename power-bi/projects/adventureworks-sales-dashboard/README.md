# AdventureWorks Sales Performance Dashboard

## Project Overview

This Power BI dashboard analyzes the commercial performance of **AdventureWorks** from **2017 to 2020**, focusing on sales, product-level profitability, regional performance, reseller behavior, pricing strategy, and KPI monitoring.

The objective of this project was not only to create visualizations, but to build a business-oriented report where each page answers a specific analytical question.

The Power BI file is included in this project folder:

```text
adventureworks-sales-performance-dashboard.pbix
```

Since `.pbix` files cannot be previewed directly on GitHub, screenshots of each report page are included below.

---

## Report Preview

> Screenshots will be added in this section.

### 1. Executive Overview

![Executive Overview](screenshots/01-executive-overview.png)

### 2. Product Category Performance

![Product Category Performance](screenshots/02-product-category-performance.png)

### 3. Product Profitability Analysis

![Product Profitability Analysis](screenshots/03-product-profitability-analysis.png)

### 4. Regional Sales Performance

![Regional Sales Performance](screenshots/04-regional-sales-performance.png)

### 5. Customer and Reseller View

![Customer and Reseller View](screenshots/05-customer-reseller-view.png)

### 6. Pricing and Margin Strategy

![Pricing and Margin Strategy](screenshots/06-pricing-margin-strategy.png)

### 7. KPI Performance

![KPI Performance](screenshots/07-kpi-performance.png)

---

## Dataset

The report uses the **AdventureWorks Sales** sample dataset.

The model follows a star-schema logic, with `Sales` as the central fact table and several dimension tables used for filtering and analysis.

### Main fact table

- `Sales`

### Main dimension tables

- `Date`
- `Product`
- `Customer`
- `Reseller`
- `SalesTerritory`
- `SalesOrder`

---

## Data Model Notes

The central table in this report is `Sales`, which contains the main commercial facts:

- Sales amount
- Product cost
- Order quantity
- Unit price
- Product keys
- Customer keys
- Reseller keys
- Territory keys
- Date keys

The report uses the relationship:

```text
Date[DateKey] → Sales[OrderDateKey]
```

This means that sales are analyzed based on the **order date**.

The `Sales` table also contains `DueDateKey`, but this field was not used as the main date relationship because the purpose of the report is to analyze sales by order date, not by due date.

In a different business analysis, `DueDateKey` could be useful for questions related to delivery, due dates, operational timelines, or fulfillment. However, for this dashboard, `OrderDateKey` is the correct field because the report focuses on when sales orders were placed.

---

## Important Data Validation Note

Although the `Date` table includes the year **2021**, the `Sales` fact table contains sales records only from **2017 to 2020** based on `OrderDateKey`.

For this reason, the report focuses on the **2017–2020 sales period**, and the KPI page is filtered to **2020**, which is the latest available year with sales data.

This was an important validation step because selecting 2021 in the date filter returns blank sales values. The presence of 2021 in the `Date` table does not mean that there are sales in 2021. It only means that the calendar table includes that year.

This distinction matters because a calendar table can contain dates that are not necessarily present in the fact table. In this case, 2021 exists in the date dimension but does not have related sales transactions through `OrderDateKey`.

---

## Core DAX Measures

The following DAX measures were created for the report.

### Total Sales

```DAX
Total Sales = SUM(Sales[Sales Amount])
```

This measure calculates total revenue from sales.

---

### Total Cost

```DAX
Total Cost = SUM(Sales[Total Product Cost])
```

This measure calculates the total product cost available in the dataset.

---

### Total Profit

```DAX
Total Profit = [Total Sales] - [Total Cost]
```

This measure calculates profit based on sales amount minus total product cost.

---

### Profit Margin

```DAX
Profit Margin = DIVIDE([Total Profit], [Total Sales])
```

This measure calculates the percentage of sales that remains after subtracting product cost.

---

### Total Quantity

```DAX
Total Quantity = SUM(Sales[Order Quantity])
```

This measure calculates the total quantity sold.

---

### Average Unit Price

```DAX
Average Unit Price = AVERAGE(Sales[Unit Price])
```

This measure is used in the pricing analysis page.

---

## Profit Interpretation

In this report, `Profit` is calculated as:

```text
Sales Amount - Total Product Cost
```

Therefore, `Profit Margin` should be interpreted as a product-level margin based on the available product cost data.

It should **not** be interpreted as net profit margin, because the dataset does not include operating expenses such as:

- Salaries
- Rent
- Utilities
- Marketing
- Taxes
- Administrative expenses
- Financial expenses

In a real business context, a full net profit analysis would require additional expense data.

This is an important limitation of the dataset. The report can analyze margin after product cost, but it cannot evaluate final company profitability after all business expenses.

---

## Target Measures

Since the dataset does not include official business targets, illustrative benchmarks were created for dashboard design purposes.

In a real business setting, these targets should be validated with the finance, commercial planning, or executive team.

---

### Target Sales

```DAX
Target Sales = 25000000
```

The sales target was set at **25M** for 2020. This was defined as a reasonable illustrative benchmark because total sales in 2020 were approximately **24.47M**.

---

### Min Sales

```DAX
Min Sales = 0
```

---

### Max Sales

```DAX
Max Sales = 50000000
```

The maximum sales value was set at **50M** to provide a readable gauge scale, considering that the highest annual sales value in the dataset was approximately **42.90M** in 2019.

---

### Target Profit Margin

```DAX
Target Profit Margin = 0.15
```

The target profit margin was set at **15%** based on the historical profit margin range.

Observed yearly profit margins:

```text
2017 → 15.77%
2018 → 9.55%
2019 → 9.97%
2020 → 14.23%
Total → 11.43%
```

The 15% target is close to the best historical performance and therefore works as an ambitious but realistic benchmark.

---

### Min Profit Margin

```DAX
Min Profit Margin = 0
```

---

### Max Profit Margin

```DAX
Max Profit Margin = 0.20
```

The maximum profit margin was set at **20%** instead of 100% because the observed margins are much lower. This makes the gauge more readable and useful.

---

# Report Pages

---

## 1. Executive Overview

### Business Question

How did AdventureWorks perform overall from 2017 to 2020 in terms of sales, profit, and margin?

### Questions Answered

- What were total sales?
- How much profit was generated?
- What was the overall profit margin?
- Which year had the strongest sales performance?
- Did profit move in the same direction as sales?
- How did the business perform across the available sales period?

### Visuals Used

- Card: Total Sales
- Card: Total Profit
- Card: General Profit Margin
- Combo chart: Total Sales and Total Profit by Year
- Slicer: Year

### Page Interpretation

The page shows total sales of approximately **109.81M**, total profit of approximately **12.55M**, and an overall profit margin of **11.43%**.

The yearly trend shows that **2019 was the strongest year in sales**, reaching approximately **42.90M**. Profit also increased from 2017 to 2019, then decreased in 2020.

This page provides a high-level executive view of the business before moving into product, regional, reseller, and pricing analysis.

### Business Observation

The overall trend suggests that sales and profit generally move in the same direction. However, the decrease in 2020 indicates that the latest available sales year performed below 2019.

This page is useful as an executive starting point because it answers the first business question:

> How is the business performing overall?

### Design Notes

Cards were used for key metrics because they allow the user to quickly understand the overall scale of the business. The combo chart was used because it compares two related measures: total sales and total profit.

The page also includes a year slicer to allow users to explore the available period from 2017 to 2020.

---

## 2. Product Category Performance

### Business Question

Which product categories generate the highest sales and profit?

### Questions Answered

- Which category sells the most?
- Which category generates the most profit?
- Does the highest-selling category also generate the highest profit?
- How concentrated are sales by category?
- Which subcategories explain most of the sales?

### Visuals Used

- Treemap: Sales by Category and Subcategory
- Bar chart: Total Profit by Category
- Slicer: Year

### Page Interpretation

The treemap shows that **Bikes** dominate total sales. The profit bar chart also shows that Bikes generate the highest total profit.

This indicates that AdventureWorks is highly dependent on the Bikes category as both a revenue and profit driver.

### Business Observation

This concentration can be positive because Bikes are clearly a strong category. However, it may also represent a business risk if the company depends too heavily on one category.

If the Bikes category experiences lower demand, supply chain problems, or pricing pressure, the overall business could be significantly affected.

### Design Notes

The treemap was used to show the composition of sales by category and subcategory. This is useful when the goal is to understand how much each group contributes to the total.

The bar chart complements the treemap by showing total profit by category. This is important because the category with the highest sales is not always the category with the highest profit.

In this case, Bikes dominate both sales and profit.

---

## 3. Product Profitability Analysis

### Business Question

Which products sell a lot but have low profitability?

### Questions Answered

- Which products generate the highest sales?
- Which products have the highest profit margin?
- Are there high-sales products with low margin?
- Which products may require price or cost review?
- Which product categories contain the most profitable products?
- Are there smaller products with strong profit margins?

### Visual Used

Scatter plot:

- X-axis: Total Sales
- Y-axis: Profit Margin
- Bubble size: Total Quantity
- Legend: Product Category
- Details: Product

### Page Interpretation

Each bubble represents a product. The position of each product shows its sales performance and profit margin, while the bubble size shows the quantity sold.

The scatter plot can be interpreted using four groups:

```text
High Sales + High Margin
→ Star products

High Sales + Low Margin
→ High-volume products that may need margin review

Low Sales + High Margin
→ Smaller but profitable products with growth potential

Low Sales + Low Margin
→ Weak or low-priority products
```

### Business Observation

This page goes beyond simply identifying top-selling products. It helps distinguish between products that generate revenue and products that are truly profitable.

Some products may have high sales but relatively low margins. Those products may require a deeper review of pricing, cost structure, or discounting strategy.

On the other hand, products with lower sales but strong margins may represent growth opportunities.

### Design Notes

A scatter plot was selected because the page compares two numerical variables at the same time: total sales and profit margin.

The size of each bubble adds a third analytical layer by showing total quantity sold.

This page also illustrates an important DAX concept: `Profit Margin` is a dynamic measure. It is not automatically calculated “by product” unless the visual provides product-level context. In this scatter plot, because `Product` is used as the detail field, Power BI evaluates the measure for each product.

---

## 4. Regional Sales Performance

### Business Question

Which regions or territories are driving sales and profitability?

### Questions Answered

- Which regions generate the highest sales?
- Which regions have the highest profit margin?
- Do high-sales regions also have strong margins?
- Are there underperforming regions?
- How is commercial performance distributed geographically?

### Visuals Used

- Map: Total Sales by Region
- Bar chart: Profit Margin by Region
- Slicer: Year

### Page Interpretation

The map provides a geographic view of sales distribution. The profit margin bar chart complements the map by allowing a more precise comparison of profitability by region.

This page shows that a region may have strong sales but not necessarily the highest margin. For this reason, sales and margin should be analyzed together.

### Business Observation

Regional performance should not be evaluated using only sales volume. A region with lower sales may still have strong profitability if its margins are higher.

Similarly, a high-sales region may require attention if its margin is weak.

### Design Notes

The map was used to provide geographic context. However, maps are not always ideal for comparing exact values. For that reason, a bar chart was included to compare profit margin by region more clearly.

This page combines geographic exploration with a more precise profitability comparison.

---

## 5. Customer and Reseller View

### Business Question

Does the business depend heavily on specific resellers or business types?

### Questions Answered

- Which reseller generates the highest sales?
- Which business type contributes the most to sales?
- Which resellers have strong profit margins?
- Are there resellers with high sales but negative or low profit?
- What does “Not Applicable” mean in the Business Type analysis?

### Visuals Used

- Table: Total Sales, Reseller, Total Profit, Profit Margin
- Treemap: Total Sales by Business Type
- Slicer: Region

### Page Interpretation

The table allows detailed comparison across resellers, including sales, profit, and profit margin.

The treemap shows sales distribution by business type. Warehouse appears as a major contributor, followed by other business types such as Value Added Reseller and Specialty Bike Shop.

### Note About “Not Applicable”

The “Not Applicable” category likely represents sales that are not associated with a specific reseller business type. This does not necessarily mean there is an error in the data.

It means that, for those sales records, the reseller business type does not apply or is not available.

Depending on the business question, this category could either be kept for transparency or filtered out if the page is focused only on reseller-specific performance.

### Business Observation

This page helps identify whether sales are concentrated in specific resellers or business types.

If a small number of resellers or business types contribute a large portion of sales, the business may depend heavily on those channels.

### Design Notes

The table provides detailed values at the reseller level. The treemap provides a more visual composition of sales by business type.

During the analysis, it was important to validate that “Not Applicable” was not necessarily an error, but a category that appears because some sales do not have an applicable reseller business type.

---

## 6. Pricing and Margin Strategy

### Business Question

Which products have a favorable or unfavorable relationship between average unit price, sales, and profit margin?

### Questions Answered

- Do higher-priced products have better margins?
- Which products have high prices but low margins?
- Which products have low prices but strong margins?
- Which categories perform better in terms of pricing and profitability?
- Do discounts explain profitability differences?

### Visuals Used

- Scatter plot: Average Unit Price vs Profit Margin
- Bubble size: Total Sales
- Legend: Product Category
- Table: Category, Product, Average Unit Price, Total Sales, Profit Margin
- Slicer: Year

### Page Interpretation

The scatter plot analyzes the relationship between product pricing and profitability.

Products with higher prices and strong margins can be considered premium and profitable. Products with high prices but weak margins may require further review of costs or pricing strategy.

The table complements the scatter plot by allowing specific products to be identified by name and value.

### Discount Analysis Note

A discount analysis was initially considered, but the `Unit Price Discount Pct` field showed little to no variation across the dataset.

For this reason, the pricing page focuses on:

- Average Unit Price
- Total Sales
- Product Cost
- Profit Margin

instead of discount impact.

This was an important analytical decision because not every available field contributes meaningful insight.

### Business Observation

The page helps identify whether price levels are aligned with profitability.

A high-priced product with low margin may indicate high product costs or pricing inefficiency. A lower-priced product with strong margin may be a good candidate for promotion or growth.

### Design Notes

The original idea was to analyze discounts and profitability. However, after validating the discount field, it became clear that discounts were not a useful driver in this dataset.

Instead of forcing a weak visual, the page was redesigned around pricing and margin strategy. This makes the analysis more meaningful.

---

## 7. KPI Performance

### Business Question

Is the business meeting its sales and profitability targets in 2020?

### Questions Answered

- Did 2020 sales reach the target?
- Did 2020 profit margin reach the target?
- How close was the business to its goals?
- How did profit margin behave throughout 2020?

### Page Filter

This page is filtered to:

```text
Date - Year = 2020
```

The page focuses on 2020 because it is the latest year with sales data in the `Sales` table.

Although the `Date` table includes 2021, there are no related sales records in 2021 using `OrderDateKey`.

### Visuals Used

- Gauge: Total Sales vs Target Sales
- KPI: Profit Margin vs Target Profit Margin
- Line chart: Profit Margin by Month

### Sales Gauge Interpretation

The gauge shows:

```text
Total Sales 2020: 24.47M
Target Sales: 25M
Max Sales: 50M
```

This means that AdventureWorks reached approximately:

```text
24.47 / 25 = 97.9%
```

of the illustrative 2020 sales target.

### Profit Margin KPI Interpretation

The KPI shows:

```text
Profit Margin 2020: 14.23%
Target Profit Margin: 15.00%
```

Power BI displays a relative difference of approximately:

```text
-5.15%
```

This does not mean that the margin is 5.15 percentage points below target.

The difference in percentage points is:

```text
15.00% - 14.23% = 0.77 percentage points
```

The `-5.15%` represents the relative gap compared with the target:

```text
(14.23% - 15.00%) / 15.00% ≈ -5.15%
```

### KPI Design Note

When using Month as the KPI trend axis, Power BI displays the latest monthly value, not the annual 2020 margin. This caused the KPI to show a much lower value for the last month.

For this reason:

```text
Gauge / KPI → best for target comparison
Line chart → best for monthly trend analysis
```

The final design separates annual target comparison from monthly trend interpretation.

### Business Observation

The KPI page shows that 2020 sales were very close to the illustrative sales target, while profit margin was slightly below the 15% benchmark.

This page provides a simple executive view of performance against goals.

### Design Notes

The KPI page is intentionally filtered to 2020 because it represents the most recent complete year of sales data in the dataset.

The sales target and profit margin target are illustrative. In a real company, these values should be provided or validated by the finance or commercial planning team.

---

# Key Business Insights

## 1. Sales peaked in 2019

The strongest sales year was 2019, with approximately **42.90M** in total sales.

## 2. 2020 sales declined but remained close to the illustrative target

Sales in 2020 reached approximately **24.47M**, close to the 25M benchmark.

## 3. Bikes dominate both sales and profit

The Bikes category is the main driver of revenue and profit.

## 4. Profit margin varies significantly by product and region

High sales do not always imply high margins. Product-level and regional margin analysis provide additional business context.

## 5. Discounts are not a major driver in this dataset

The discount field showed little to no variation, so discount analysis was not useful as a main page.

## 6. Targets are illustrative

The sales and margin targets were created for dashboard design purposes. In a real company, they should be defined by finance, planning, or leadership teams.

---

# Dashboard Design Principles Applied

This report was designed using the following principles:

- One main business question per page
- Clear separation between overview, product, region, reseller, pricing, and KPI analysis
- Use of cards for executive metrics
- Use of scatter plots for profitability analysis
- Use of treemaps for composition analysis
- Use of gauges and KPIs for target monitoring
- Use of slicers and page-level filters for context
- Consistent color palette
- Reduced cognitive load
- Visuals selected based on the question being answered

---

# Project Limitations

## 1. No official targets were available

The dataset does not include official sales or margin targets. The targets used in this report were created as illustrative benchmarks.

## 2. Profit is not net profit

The profit calculation does not include operating expenses, taxes, salaries, rent, utilities, or marketing costs.

## 3. 2021 exists in the Date table but not in Sales

The calendar table includes 2021, but the sales fact table does not contain related sales records for 2021 using `OrderDateKey`.

## 4. Discount analysis was limited

The discount field had little to no variation, so it was not useful as a primary analytical dimension.

---

# How I Would Present This Project

This dashboard analyzes AdventureWorks sales performance from 2017 to 2020 using Power BI.

I built the report around a star-schema model, with `Sales` as the fact table and dimensions such as `Date`, `Product`, `Reseller`, and `SalesTerritory`.

Before building the visualizations, I validated the available date range and found that although the `Date` table includes 2021, the `Sales` table contains sales only through 2020 based on `OrderDateKey`. For this reason, the report focuses on 2017–2020, and the KPI page uses 2020 as the latest available year.

I created DAX measures for Total Sales, Total Cost, Total Profit, Profit Margin, Total Quantity, and Average Unit Price. I also created illustrative targets for sales and profit margin to practice KPI and gauge visuals.

The report is organized by business question:

```text
Executive Overview
→ How is the business performing overall?

Product Category Performance
→ Which categories drive sales and profit?

Product Profitability Analysis
→ Which products sell a lot but have low margin?

Regional Sales Performance
→ Which regions perform best?

Customer and Reseller View
→ Which resellers and business types contribute most to sales?

Pricing and Margin Strategy
→ How do price, sales, and margin relate?

KPI Performance
→ Is the business meeting 2020 sales and margin targets?
```

The goal was to create a dashboard that is not only visually clear, but also easy to explain from a business perspective.

---

# Repository Contents

```text
adventureworks-sales-dashboard/
│
├── README.md
├── adventureworks-sales-performance-dashboard.pbix
└── screenshots/
    ├── 01-executive-overview.png
    ├── 02-product-category-performance.png
    ├── 03-product-profitability-analysis.png
    ├── 04-regional-sales-performance.png
    ├── 05-customer-reseller-view.png
    ├── 06-pricing-margin-strategy.png
    └── 07-kpi-performance.png
```

---

# Tools Used

- Power BI Desktop
- DAX
- Data modeling
- Star schema logic
- Data visualization
- Dashboard design principles
- GitHub documentation

---

# Final Reflection

This project helped me practice the full Power BI workflow: validating data, understanding relationships, creating DAX measures, selecting visuals based on business questions, applying filters, designing report pages, and documenting insights.

The most important learning was that building a dashboard is not only about creating charts. It is about translating business questions into clear, useful, and well-structured visual analysis.

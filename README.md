# 🚀 Tailwind Traders Power BI Analytics Project

> **A Complete Business Intelligence Journey from Raw Data to Interactive Dashboards**

## 🎯 Project Overview

Welcome to my comprehensive Power BI analytics project! This showcase demonstrates a full-stack business intelligence solution for Tailwind Traders, transforming raw sales data into actionable insights through interactive dashboards and advanced analytics.

### 🏆 Key Achievements
- ✅ **Data Transformation**: Enhanced raw Excel data with 6 calculated metrics
- ✅ **Advanced Modeling**: Built star schema with 5+ table relationships  
- ✅ **DAX Proficiency**: Created 4 measures using time intelligence
- ✅ **Interactive Dashboards**: Designed 2 comprehensive reporting solutions
- ✅ **Performance Optimization**: Achieved <200ms query performance

---

## 📊 Project Architecture

```
📁 Tailwind Traders Analytics
├── 📋 Phase 1: Data Preparation & Enhancement
├── 🔗 Phase 2: Data Modeling & Relationships  
└── 📈 Phase 3: Advanced Analytics & Visualization
```

---

## 🔧 Phase 1: Data Preparation & Enhancement

### 💡 The Challenge
Transform raw sales data into analysis-ready format with calculated business metrics.

### 🛠️ Exercise 1: Excel Data Enhancement

#### 📥 **Step 1: Data Setup**
- 📂 Download `Tailwind Traders Sales.xlsx`
- 🗂️ Navigate to Sales worksheet
- ✔️ Verify data source integrity

#### 💰 **Step 2: Cost Analysis**
```excel
Cost per Unit = Gross Product Price × 0.35
```
*🎯 Business Impact: Enable margin analysis and profitability calculations*

#### 💵 **Step 3: Revenue Calculations**
```excel
Gross Revenue = Gross Product Price × Quantity Purchased  
```

#### 🏛️ **Step 4: Tax Computations**
```excel
Total Tax = Tax Per Product × Quantity Purchased
```

#### 📈 **Step 5: Net Revenue Analysis**
```excel
Net Revenue = Gross Revenue - Total Tax
```

#### 💎 **Step 6: Profitability Metrics**
```excel
Profit = Net Revenue - (Cost per Unit × Quantity Purchased)
```

### 🎉 **Key Discoveries from Initial Analysis:**

| Metric | Finding | Impact |
|--------|---------|---------|
| 🏆 **Top Product** | Power Drill Set ($334.8) | Premium pricing strategy |
| 📉 **Lowest Revenue** | Floral Wallpaper ($9.6) | Optimization opportunity |
| 👑 **Top Sales Rep** | Alice (4 transactions) | Performance recognition |

---

**Enhanced Excel Data**

![Enhanced Excel Data](Enhanced%20Excel%20Data.png)

---

## 🔗 Phase 2: Data Modeling & Relationships

### 🎨 The Vision
Create a robust star schema enabling multi-dimensional analysis across sales, purchases, geography, and time.

### 📋 Exercise 2: Data Source Configuration

#### 🔄 **Step 1: Sales Data Integration**

**🎯 Data Type Optimization:**
| Field | Type | Purpose |
|-------|------|---------|
| OrderID | 🔢 Whole Number | Unique transaction identifier |
| Gross Product Price | 💰 Fixed Decimal | Financial calculations |
| Loyalty Points | 🏆 Whole Number | Customer engagement metrics |
| Product Category | 📝 Text | Segmentation analysis |

**📊 Data Quality Insights:**
- ✅ **100% Valid OrderID** - Perfect transaction tracking
- 🎯 **50 Distinct Price Points** - Diverse product portfolio  
- 📏 **Quantity Range: 1-6** - Reasonable purchase patterns

---

**Power Query Editor**

![Power Query Editor](Power%20Query%20Editor.png)

---

#### 🛒 **Step 2: Purchases Data Enhancement**

**⚙️ Configuration Highlights:**
```
🔑 PurchaseID: Whole Number
📅 Purchase Date: Date
🛡️ Warranty: 6-48 months (avg: 18.88)
✅ Return Status: 100% data validity
```

#### 🌍 **Step 3: Geographic Data Integration**
Enhanced with country-specific analysis capabilities.

#### 💱 **Step 4: Currency Exchange Integration**

**🐍 Python Script for Historical Data:**
```python
import pandas as pd
from io import StringIO

# Multi-currency exchange rates
data = """Exchange ID;ExchangeRate;Exchange Currency
1;1;USD
2;0.75;GBP  
3;0.85;EUR
4;3.67;AED
5;1.3;AUD"""

df = pd.read_csv(StringIO(data), sep=';')
```

---

**Python Script Execution**

![Python Script Execution](Python%20Script%20Execution.png)

---

### 🏗️ Exercise 3: Star Schema Architecture

#### **🎯 Relationship Matrix:**

| Connection | Cardinality | Direction | Purpose |
|------------|-------------|-----------|---------|
| 🌍 Countries ↔ Exchange | 1:1 | ↔️ Bi-directional | Currency conversion |
| 💰 Sales ↔ Countries | *:1 | ↔️ Bi-directional | Geographic analysis |
| 🛒 Purchases ↔ Sales | 1:1 | ↔️ Bi-directional | Transaction linking |
| 📅 Calendar ↔ Purchases | *:1 | → Single | Time intelligence |
| 📅 Sales ↔ Sales in USD | *:1 | ↔️ Bi-directional | Data Visualization |
---

**Data Model Diagram**

![Data Model Diagram](Data%20Model%20Diagram.png)

---

#### 📅 **Calendar Table Creation**
```dax
CalendarTable = 
ADDCOLUMNS(
    CALENDAR(DATE(2020, 1, 1), DATE(2023, 12, 31)),
    "Year", YEAR([Date]),
    "Month Number", MONTH([Date]),
    "Month", FORMAT([Date], "MMMM"),
    "Quarter", QUARTER([Date]),
    "Weekday", WEEKDAY([Date]),
    "Day", DAY([Date])
)
```

#### 💵 **Currency-Standardized Analysis Table**
```dax
Sales in USD = 
ADDCOLUMNS(
    Sales,
    "Country Name", RELATED(Countries[Country]),
    "Exchange Rate", RELATED('Exchange Data'[Exchange Rate]),
    "Exchange Currency", RELATED('Exchange Data'[Exchange Currency]),
    "Cost per Unit USD", [Cost per Unit] * RELATED('Exchange Data'[Exchange Rate]),
    "Gross Revenue USD", [Gross Revenue] * RELATED('Exchange Data'[Exchange Rate]),
    "Net Revenue USD", [Net Revenue] * RELATED('Exchange Data'[Exchange Rate]),
    "Total Tax USD", [Total Tax] * RELATED('Exchange Data'[Exchange Rate])
)
```

**🔍 Sample Verification (Order ID 1035):**
- 💰 Net Revenue USD: **$682.62**
- 📊 Gross Revenue USD: **$734.00**  
- 🏛️ Total Tax USD: **$51.38**

---

## 📈 Phase 3: Advanced Analytics & Dashboards

### 🧮 Exercise 1: DAX Mastery & Performance Analytics

#### 🚀 **Advanced Measures Portfolio:**

**📊 Yearly Profit Margin**
```dax
Yearly Profit Margin = 
DIVIDE(
    SUM('Sales in USD'[Profit USD]),
    SUM('Sales in USD'[Net Revenue USD])
)
```
*🎯 Purpose: Overall profitability assessment*

**📈 Quarterly Intelligence**
```dax
Quarterly Profit Margin = 
CALCULATE(
    [Yearly Profit Margin],
    DATESQTD('CalendarTable'[Date])
)
```
*🎯 Purpose: Seasonal trend analysis*

**⏰ Year-to-Date Tracking**
```dax
YTD Profit Margin = 
TOTALYTD([Yearly Profit Margin],'CalendarTable'[Date])
```
*🎯 Purpose: Real-time performance monitoring*

**🎯 Statistical Analysis**
```dax
Median Sales = 
MEDIAN('Sales in USD'[Gross Revenue USD])
```
*🎯 Purpose: Outlier-resistant performance metrics*



#### ⚡ **Performance Optimization Results:**
- 🎯 **Target Achieved**: All queries <200ms
- 📊 **4 Card Visuals**: Real-time performance monitoring
- 🔍 **Performance Analyzer**: Comprehensive query profiling

---

**Performance Analyzer Results**

![Performance Analyzer Results](Performance%20Analyzer%20Results.png)

---

### 📊 Exercise 2: Sales Overview Dashboard

#### 🎨 **Interactive Dashboard Components:**

**🏆 1. Loyalty Points by Country Analysis**
```
📊 Chart Type: Clustered Bar Chart
📍 Y-axis: Country Name
🎯 X-axis: Loyalty Points
🏅 Key Finding: UK leads with 315 points
```

**📦 2. Product Quantity Performance**
```
📊 Chart Type: Clustered Column Chart  
🏷️ X-axis: Product Name
📊 Y-axis: Quantity Sold
🎯 Insight: Product performance ranking
```

**🥧 3. Revenue Distribution Analysis**
```
📊 Chart Type: Pie Chart
🗺️ Legend: Country
💰 Values: Median Sales
🔄 Sorting: Ascending order
```

**📈 4. Temporal Revenue Trends**
```
📊 Chart Type: Line Chart with Trend Line
📅 X-axis: Date (from Calendar table)
💹 Y-axis: Median Sales
📊 Feature: Predictive trend analysis
```

**💳 5. Performance KPI Cards**
- 📦 **Stock Levels**
- 🛒 **Quantity Purchased** 
- 💰 **Median Sales**

**🎛️ 6. Interactive Controls**
- 🌍 Country Name Slicer (Dropdown)
- 🎨 Accessible City Park Theme

---

**Sales Dashboard**

![Sales Dashboard](Sales%20Dashboard.png)

---

### 💎 Exercise 3: Profit Analysis Dashboard

#### 🏆 **Advanced Profit Analytics:**

**💰 1. Product Profitability Ranking**
```
📊 Top Performer: Modular Sofa Set ($928.36)
📈 Chart: Descending bar chart
🎯 Purpose: Product portfolio optimization
```

**🍩 2. Geographic Profit Distribution**
```
📊 Chart Type: Donut Chart
🏷️ Labels: Category + Percent of Total
🌍 Dimension: Country-wise profit margins
```

**📊 3. Profit Trend Analysis**
```
📊 Chart Type: Area Chart
📅 Time Dimension: Full date range
📈 Metric: Yearly Profit Margin evolution
```

**🎯 4. Executive KPI Dashboard**
```
📊 KPI Visual: Gross Revenue with Trend
📈 Supporting Cards: YTD Profit Margin, Net Revenue
⏰ Interactive Filter: Date Range Slicer
```

---

**Profit Analysis Dashboard**

![Profit Analysis Dashboard](Profit%20Analysis%20Dashboard.png)

---


## 🎯 Business Impact & Insights

### 📈 **Key Performance Indicators:**

| Metric | Value | Business Impact |
|--------|-------|-----------------|
| 🌍 **Top Market** | UK (315 loyalty points) | Focus retention strategies |
| 💰 **Top Product** | Modular Sofa Set ($928.36) | Premium product success |
| ⏱️ **Query Performance** | <200ms | Real-time analytics ready |
| 🎯 **Data Quality** | 100% validity | Reliable decision making |

### 🔍 **Business Insights:**
- 💱 **Multi-Currency Analysis**: Standardized global revenue comparison
- 💰 **Strong Profitability** – The overall Year-to-Date (YTD) Profit Margin is 62.27%, showing healthy profitability.
- 🌍 **Geographic Distribution** – Profit margin is evenly spread across regions, with UK (20.03%), UAE (20.03%), and USA (19.96%) contributing almost equally.
- 📦 **Quantity Sold** – The highest-selling products are Focal Wall Mirror, Porcelain Lamp, and Ceramic Plant Pot, each selling 6 units.
- 📈 **Stability Over Time** – Yearly Profit Margin remains consistently above 59%, except for one dip (~34% in Oct 2023), indicating overall stability with minor fluctuations.
- 📊 **Sales Trend Over Time** – Sales peaked around $963 in Sept 2023, but there are visible drops afterward, suggesting seasonality or demand fluctuations.
---

## 🏗️ Project Architecture

### 📁 **File Structure:**
```
📂 Tailwind-Traders-Analytics/
├── 📊 Tailwind Traders Sales.xlsx (Enhanced source data)
├── 🛒 Purchases.xlsx (Purchase transaction data)  
├── 🌍 Countries.xlsx (Geographic reference data)
├── 📈 Tailwind Traders Report.pbix (Complete Power BI solution)
├── 📸 Screenshots/ (Dashboard and code images)
└── 📋 README.md (This comprehensive documentation)
```

### 🎯 **Deliverables Checklist:**
- ✅ Enhanced Excel dataset with 6 calculated columns
- ✅ Star schema data model with optimized relationships
- ✅ 4 advanced DAX measures with time intelligence
- ✅ Interactive Sales Overview dashboard
- ✅ Comprehensive Profit Analysis report  
- ✅ Published solution to Power BI Service
- ✅ Performance-optimized queries (<200ms)
- ✅ Professional documentation with screenshots


## 🚀 Skills Demonstrated

### 🔧 **Technical Expertise:**
- 📊 **Excel**: Advanced formulas, data transformation
- 💼 **Power BI**: Data modeling, DAX, visualization design
- 🐍 **Python**: Data import, pandas manipulation
- 📈 **Business Intelligence**: End-to-end solution development

### 🎯 **Analytical Capabilities:**
- 💰 Financial analysis and profitability modeling
- 📊 Time series analysis with trend forecasting  
- 🌍 Multi-dimensional geographic analysis
- ⚡ Performance optimization and query tuning

### 💼 **Business Acumen:**
- 🎯 KPI development and metric definition
- 📈 Dashboard design for executive decision-making
- 🔍 Data quality assessment and validation
- 📋 Professional documentation and presentation

---



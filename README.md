# 🚚 Olist — Delivery Delays & Customer Satisfaction Analysis

> **An end-to-end data analytics project investigating delivery performance, operational bottlenecks, and the impact of delivery delays on customer satisfaction in Brazilian e-commerce.**

---

## 📌 Project Overview

Delivery performance is a critical component of the customer experience in e-commerce. A delayed order does not only represent an operational issue — it can directly affect customer perception, ratings, brand reputation, and potentially future purchasing behavior.

This project analyzes the **Brazilian E-Commerce Public Dataset by Olist** to investigate delivery performance and understand how delivery delays relate to customer satisfaction.

The project follows an end-to-end analytics workflow:

**Data Scoping → MySQL → Analytical View → Python → Feature Engineering → Business Analysis → Excel Dashboard → Insights & Recommendations**

The analysis focuses on three main dimensions:

* 🚚 **Logistics Performance** — identifying sellers and regions with the highest delay rates and longest delays.
* ⭐ **Customer Satisfaction** — measuring how delivery delays relate to customer ratings.
* 🗺️ **Geographic Performance** — identifying regional patterns in delivery delays.

The project was developed as a portfolio case study focused on applying practical data analytics, SQL, Python, data modeling, exploratory analysis, and business intelligence concepts.

---

# 🎯 Business Problem

Delivery delays are a common challenge in e-commerce operations and can have consequences beyond the logistics process itself.

The main business question investigated in this project is:

> **How do delivery delays affect customer satisfaction, and where are the main operational bottlenecks?**

To answer this question, the analysis investigates:

* How frequently are orders delivered late?
* How severe are delivery delays?
* Which sellers have the highest delay rates?
* Which sellers have the longest average delays?
* Which states experience the highest frequency of delays?
* Which states experience the longest delays?
* How does customer satisfaction differ between delayed and on-time orders?
* How does the probability of receiving the lowest possible rating change when an order is delayed?

---

# 🎯 Project Objectives

The project was designed around four main objectives:

### 1. Measure logistics performance

Create operational KPIs capable of describing delivery efficiency and the accuracy of estimated delivery dates.

### 2. Identify operational bottlenecks

Analyze sellers and geographic regions to identify where delivery problems are more frequent or more severe.

### 3. Quantify the relationship between delays and customer satisfaction

Compare customer ratings between delayed and on-time orders and measure the probability of extremely negative evaluations.

### 4. Translate analytical results into business insights

Transform the analysis into actionable recommendations for logistics management and customer experience improvement.

---

# 🗂️ Dataset

The project uses the **Brazilian E-Commerce Public Dataset by Olist**, a public dataset containing information about orders placed through the Olist Brazilian e-commerce marketplace.

The original dataset is composed of multiple relational tables covering areas such as:

* Orders
* Customers
* Order items
* Products
* Reviews
* Sellers
* Payments
* Geolocation

Rather than using the entire dataset, the project deliberately reduced its scope to the variables required to answer the defined business questions.

This scoping decision was important because it reduced unnecessary data processing and created a focused analytical dataset centered on:

**Orders + Logistics + Products + Customer Reviews + Geography**

### Data source

**Brazilian E-Commerce Public Dataset by Olist — Kaggle**

The original dataset is publicly available through Kaggle under the Brazilian E-Commerce Public Dataset by Olist.

---

# 🏗️ Data Architecture & Scoping

The project began by defining the analytical scope and identifying only the tables and fields required for the analysis.

The selected data was consolidated into an analytical MySQL view named:

```text
vw_olist_full
```

The analytical view combines information from the following source tables:

```text
orders
   │
   ├── order_items
   │       │
   │       └── products
   │
   ├── order_reviews
   │
   └── customers
```

This structure allowed logistics, product, customer satisfaction, and geographic information to be analyzed together at the order level.

### Analytical tables

#### `orders`

Core logistics information:

* `order_id`
* `customer_id`
* `order_status`
* `order_purchase_timestamp`
* `order_approved_at`
* `order_delivered_carrier_date`
* `order_delivered_customer_date`
* `order_estimated_delivery_date`

#### `order_items`

Order and product information:

* `order_id`
* `product_id`
* `price`
* `freight_value`

#### `order_reviews`

Customer satisfaction information:

* `order_id`
* `review_score`
* `review_comment_message`

#### `products`

Product characteristics:

* `product_id`
* `product_category_name`
* `product_weight_g`
* `product_length_cm`
* `product_height_cm`
* `product_width_cm`

#### `customers`

Geographic information:

* `customer_id`
* `customer_city`
* `customer_state`
* `customer_zip_code_prefix`

---

# 🔄 Data Pipeline

The analytical workflow can be summarized as follows:

```text
Brazilian E-Commerce Public Dataset
              │
              ▼
          MySQL / Olist DB
              │
       Data Scoping & SQL
              │
              ▼
        vw_olist_full
              │
              ▼
      SQLAlchemy + PyMySQL
              │
              ▼
        Extract.ipynb
              │
              ▼
       vw_olist_full.csv
              │
              ▼
        Análise.ipynb
              │
       ┌──────┼───────┐
       ▼      ▼       ▼
    Cleaning Features Analysis
       │      │       │
       └──────┼───────┘
              ▼
     Analytical CSV Tables
              │
              ▼
        Excel Dashboard
              │
              ▼
     Business Insights
```

---

# 🧮 Data Preparation & Feature Engineering

After extracting the analytical view into Python, the dataset was prepared for analysis using **pandas**.

The analytical process included:

* Data cleaning
* Variable renaming
* Data type preparation
* Creation of operational metrics
* Creation of customer satisfaction indicators
* Aggregation by seller and state
* Generation of analytical datasets for the dashboard

Several derived variables were created to support the analysis.

### Delivery time

Measures the number of days between the purchase and the actual delivery:

```text
delivery_time_days =
order_delivered_customer_date
-
order_purchase_timestamp
```

### Processing time

Measures the time between purchase and order approval:

```text
processing_time_days =
order_approved_at
-
order_purchase_timestamp
```

### Late delivery flag

Identifies whether an order was delivered after the estimated delivery date:

```text
late_delivery_flag = 1
when actual delivery > estimated delivery
```

Additional analytical variables were also created for:

* Order total value
* Number of items per order
* Average item price
* Average freight value
* Satisfaction level
* Presence of review comments
* Product volume
* Monthly aggregation
* Geographic grouping

---

# 📊 Key Metrics

The project uses a set of operational and customer experience metrics to evaluate delivery performance.

### Delivery Delay Rate

Percentage of delivered orders that arrived after the estimated delivery date.

### Average Delay

Average number of days of delay among orders classified as delayed.

### Average Actual Delivery Time

Average number of days between purchase and actual delivery.

### Average Estimated Delivery Time

Average delivery time estimated to the customer.

### Estimated vs. Actual Delivery Difference

Measures the difference between the estimated and actual delivery times, providing an indication of the accuracy of delivery expectations.

### Average Customer Score

Average review score associated with analyzed orders.

### Probability of Rating 1

Probability that an order receives the lowest possible customer rating.

---

# 📈 Dashboard & Analysis

The final results were presented through an interactive Excel dashboard divided into three analytical areas.

---

## 🚚 1. Logistics Performance

The logistics dashboard focuses on seller-level operational performance.

### Top 10 Sellers by Delay Rate

Ranks sellers according to the percentage of their orders delivered late.

This metric highlights sellers where delivery delays occur most frequently.

### Top 10 Sellers by Average Delay

Ranks sellers according to the average number of days of delay.

This metric focuses on the **severity** of the problem rather than its frequency.

Together, these analyses provide two complementary perspectives:

> **How often does a seller experience delays?**

and

> **How severe are those delays when they occur?**

This distinction helps identify different types of operational problems that would not be visible through a single metric.

---

# ⭐ 2. Delivery Delay & Customer Satisfaction

This section investigates the relationship between delivery performance and customer experience.

### Average Customer Score — Delayed vs. On-Time

Compares the average customer rating between:

* Orders delivered on time
* Orders delivered late

The analysis shows a substantial difference in customer perception between the two groups.

### Probability of Rating 1 — Delayed vs. On-Time

Measures the probability of receiving the lowest possible customer rating under each delivery scenario.

This analysis is particularly relevant because it goes beyond comparing averages.

Instead of asking only:

> "Do delayed orders receive lower ratings?"

it also asks:

> "How much does the risk of an extremely negative customer experience increase when an order is delayed?"

---

# 🗺️ 3. Geographic Performance

The geographic dashboard investigates how delivery performance varies across Brazilian states.

### Top 10 States by Delay Rate

Identifies the states where late deliveries occur most frequently.

### Top 10 States by Average Delay

Identifies the states where delays are longest when they occur.

This analysis highlights an important distinction between:

* **High-frequency delays**
* **High-severity delays**

A region may experience frequent delays without having the longest average delay, while another region may experience fewer delays that are significantly longer when they occur.

---

# 🔎 Key Findings

## Logistics Performance

The seller analysis revealed significant differences in delivery performance.

A subset of sellers presented **considerably higher delay rates and average delays** than the rest of the analyzed sellers.

This indicates that delivery problems are not uniformly distributed across the marketplace.

Instead, specific sellers represent potential operational bottlenecks and may benefit from targeted monitoring and corrective actions.

---

## Geographic Performance

The geographic analysis revealed distinct regional patterns.

States in the **Northeast**, including:

* Alagoas (AL)
* Maranhão (MA)
* Sergipe (SE)
* Piauí (PI)

presented some of the highest delay rates.

Meanwhile, the highest average delays were concentrated primarily in **Northern states**, including:

* Roraima (RR)
* Amapá (AP)
* Amazonas (AM)

This suggests two different operational patterns:

### Northeast

Higher frequency of delivery delays.

### North

Longer delays when delivery problems occur.

These differences indicate that logistics strategies should not necessarily be uniform across all regions.

---

# ⭐ Customer Satisfaction Findings

The strongest relationship identified in the project was the association between delivery delays and customer satisfaction.

Orders delivered on time presented an average customer score of approximately:

**4.1 / 5**

while delayed orders presented an average score of approximately:

**2.5 / 5**

This represents a decrease of approximately:

**39%**

in average customer rating.

The probability of receiving the lowest possible rating also changed substantially:

```text
On-time orders     → ~10%
Delayed orders     → ~45%
```

In other words, delayed orders showed approximately a:

**4.5× higher probability of receiving a rating of 1.**

These results indicate a strong relationship between delivery performance and negative customer experiences.

---

# 💼 Business Implications

The findings suggest that delivery delays can affect the business across several dimensions.

### Operational efficiency

High delay rates may indicate bottlenecks in seller operations, processing, transportation, or regional logistics.

### Customer experience

Delayed orders are associated with substantially lower customer ratings and a significantly higher probability of extremely negative evaluations.

### Reputation

A concentration of poor ratings associated with delivery problems can negatively affect customer perception and trust.

### Financial impact

Poor customer experiences may contribute indirectly to higher support costs, lower retention, and increased customer acquisition pressure.

The analysis therefore suggests that delivery performance should be treated not only as an operational KPI, but also as a **customer experience indicator**.

---

# 💡 Recommendations

Based on the analytical findings, several actions can be considered.

### 1. Prioritize underperforming sellers

Sellers with the highest delay rates and longest average delays should receive targeted operational monitoring.

### 2. Establish seller-level performance targets

Delay rate and average delay can be incorporated into recurring seller performance monitoring.

### 3. Develop regional logistics strategies

Different regional patterns suggest that operational strategies should consider geographic characteristics rather than applying a single approach to all locations.

### 4. Improve delivery estimates

Estimated delivery dates should reflect actual operational performance as closely as possible.

More accurate estimates can reduce the gap between customer expectations and actual delivery performance.

### 5. Proactively communicate delivery risks

Orders identified as having a high probability of delay could trigger proactive customer communication.

This may help reduce frustration even when a delay cannot be completely avoided.

### 6. Monitor customer experience alongside logistics KPIs

Delivery performance should be analyzed together with customer satisfaction metrics.

A logistics KPI alone may show that delays are increasing, while customer ratings reveal the actual business consequence of that deterioration.

---

# 🛠️ Technologies

The project combines relational data management, Python-based analysis, and business intelligence.

| Technology           | Purpose                                                             |
| -------------------- | ------------------------------------------------------------------- |
| **MySQL**            | Data scoping, relational modeling, and analytical view creation     |
| **SQL**              | Data selection, joins, filtering, and analytical view construction  |
| **Python**           | Data preparation, transformation, feature engineering, and analysis |
| **pandas**           | Data manipulation and analytical processing                         |
| **SQLAlchemy**       | Database connection and data extraction                             |
| **PyMySQL**          | MySQL connectivity                                                  |
| **Jupyter Notebook** | Data extraction and analytical workflow                             |
| **Microsoft Excel**  | Interactive dashboards and data visualization                       |

---

# 📁 Project Structure

```text
PROJETO-EXCEL/
│
├── Arquivos/
│   ├── Extract.ipynb
│   └── vw_olist_full.csv
│
├── Projeto/
│   ├── Análise.ipynb
│   ├── Dashboard.xlsx
│   └── Insights.MD
│
├── Tabelas/
│   ├── atraso_vs_score.csv
│   ├── atrasos_por_estado.csv
│   ├── atrasos_por_seller.csv
│   ├── kpis_gerais.csv
│   ├── olist_tratada.csv
│   └── probabilidade_nota1.csv
│
├── Mapa da base analítica Olist.txt
├── .gitattributes
└── README.md
```

### `Arquivos/`

Contains the data extraction workflow and the analytical view exported from MySQL.

* `Extract.ipynb` — Python notebook responsible for connecting to MySQL and extracting the `vw_olist_full` analytical view using SQLAlchemy and PyMySQL.
* `vw_olist_full.csv` — exported analytical dataset used as the input for the Python analysis.

### `Projeto/`

Contains the main analytical and visualization artifacts.

* `Análise.ipynb` — main analytical notebook containing data preparation, feature engineering, KPI calculations, and analyses.
* `Dashboard.xlsx` — interactive Excel dashboard containing logistics, customer satisfaction, and geographic analyses.
* `Insights.MD` — documented interpretation of the results, business implications, and recommendations.

### `Tabelas/`

Contains the analytical datasets generated during the Python workflow.

* `atraso_vs_score.csv` — customer score comparison between delayed and on-time orders.
* `atrasos_por_estado.csv` — delay metrics aggregated by state.
* `atrasos_por_seller.csv` — delay metrics aggregated by seller.
* `kpis_gerais.csv` — general operational KPIs.
* `olist_tratada.csv` — treated analytical dataset.
* `probabilidade_nota1.csv` — probability of receiving rating 1 for delayed and on-time orders.

### `Mapa da base analítica Olist.txt`

Documents the structure of the analytical dataset, including the selected source fields and derived variables.

---

# 📚 Analytical Questions

The project was built around a defined set of business questions:

### Logistics

* What percentage of orders were delivered late?
* What is the average delay in days?
* Which sellers have the highest delay rates?
* Which sellers have the longest average delays?

### Geography

* Which states have the highest delay rates?
* Which states experience the longest delays?
* Are delay patterns consistent across different regions?

### Customer Experience

* How does the average customer rating differ between delayed and on-time orders?
* How does the probability of receiving a rating of 1 change when an order is delayed?
* How strongly are delivery delays associated with negative customer experiences?

---

# 📊 Main Analytical Outputs

The analysis generated dedicated datasets to support the final dashboard:

```text
kpis_gerais
        │
        ├── Overall logistics KPIs
        │
atrasos_por_seller
        │
        ├── Seller performance
        │
atrasos_por_estado
        │
        ├── Geographic performance
        │
atraso_vs_score
        │
        ├── Delivery delay vs. customer rating
        │
probabilidade_nota1
        │
        └── Probability of extreme negative rating
```

This separation allowed the analytical process and dashboard layer to remain organized and reproducible.

---

# 🤖 AI-Assisted Development

The project was primarily designed, developed, and analyzed by me.

Artificial intelligence was used as a **supporting tool**, particularly for:

* Reviewing SQL queries
* Reviewing Python code
* Discussing relational modeling and data preparation practices
* Suggesting technical improvements
* Supporting documentation and project organization

The analytical decisions, business questions, data scope, metrics, interpretation, and final project structure were defined and implemented as part of the project development process.

---

# 🔐 Security

Database credentials were removed from the project files before publication.

No passwords, authentication credentials, or other sensitive connection information are included in the repository.

---

# 🎓 Project Purpose

This project was developed as a practical portfolio case study to strengthen skills in:

* SQL
* Relational data modeling
* Data extraction
* Python
* pandas
* Feature engineering
* Exploratory data analysis
* KPI development
* Business analysis
* Data visualization
* Excel dashboards
* Translating analytical findings into business recommendations

Rather than focusing solely on visualization, the project emphasizes the complete analytical process — from defining the scope of a raw dataset to transforming data into actionable business insights.

---

# 🏁 Conclusion

The analysis demonstrates that delivery performance is closely associated with customer experience.

The results reveal substantial differences in logistics performance across sellers and geographic regions, while the comparison between delayed and on-time orders shows a significant deterioration in customer ratings when delivery expectations are not met.

The strongest finding is the increase in the probability of receiving the lowest possible customer rating:

**~10% for on-time orders → ~45% for delayed orders.**

This represents approximately a **4.5× increase in the risk of an extremely negative evaluation**.

The findings reinforce the importance of treating logistics performance and customer satisfaction as interconnected dimensions of e-commerce performance.

Ultimately, the project demonstrates how a structured analytical workflow can transform operational data into insights capable of supporting decisions around **seller management, regional logistics, delivery estimation, and customer experience**.

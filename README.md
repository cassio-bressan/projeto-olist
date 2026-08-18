# Olist — Delivery Delays & Customer Satisfaction Analysis

> An end-to-end data analytics project analyzing delivery performance and its relationship with customer satisfaction using the Brazilian E-Commerce Public Dataset by Olist.

**[View the Dashboard](#)** · **[View the Analytical Notebook](#)**

---

## Project Overview

This project analyzes delivery performance in a Brazilian e-commerce marketplace, with a particular focus on understanding how delivery delays affect customer satisfaction.

The analysis was developed using the **Brazilian E-Commerce Public Dataset by Olist** and follows an end-to-end data analytics workflow, from data scoping and relational data preparation to feature engineering, exploratory analysis, business intelligence, and insight generation.

The project combines:

* MySQL for data scoping and analytical view creation;
* SQL for relational data preparation;
* Python and pandas for data treatment and analysis;
* SQLAlchemy and PyMySQL for database extraction;
* Microsoft Excel for interactive dashboards and visualization.

The main analytical focus is divided into three areas:

1. **Logistics Performance** — identifying sellers with the highest frequency and severity of delivery delays;
2. **Customer Satisfaction** — measuring the relationship between delivery delays and customer ratings;
3. **Geographic Performance** — identifying states with the highest delay rates and longest delays.

The objective is not only to measure operational performance, but to connect logistics indicators with their potential impact on the customer experience.

---

## Business Context

In e-commerce, delivery performance is an important component of the customer experience.

A delayed order can represent more than an operational inefficiency. When delivery expectations are not met, customer satisfaction may deteriorate, increasing the likelihood of negative reviews and potentially affecting customer retention and marketplace reputation.

Based on this context, the project investigates the following central business question:

> **How do delivery delays affect customer satisfaction, and where are the main operational bottlenecks?**

To answer this question, the analysis examines delivery performance across sellers and geographic regions and compares customer satisfaction between delayed and on-time orders.

---

## Business Objectives

The project was designed around four main objectives:

### 1. Measure delivery performance

Calculate operational indicators capable of describing delivery efficiency, delay frequency, delay severity, and the difference between estimated and actual delivery times.

### 2. Identify operational bottlenecks

Determine which sellers and states present the most critical delivery performance.

### 3. Evaluate the impact on customer satisfaction

Compare customer ratings between delayed and on-time orders and measure the change in the probability of receiving the lowest possible rating.

### 4. Generate actionable insights

Translate the analytical results into recommendations related to seller management, regional logistics, delivery estimates, and customer experience.

---

## Dataset

The project uses the **Brazilian E-Commerce Public Dataset by Olist**, a publicly available dataset containing information about orders placed through the Olist Brazilian e-commerce marketplace.

The original dataset contains multiple relational tables covering orders, customers, sellers, products, reviews, payments, and other aspects of the marketplace operation.

Instead of processing the entire dataset, the project began with a deliberate **scope definition**. Only the tables and fields necessary to answer the business questions were selected.

The final analytical scope focused on five main entities:

| Source table    | Analytical purpose                       |
| --------------- | ---------------------------------------- |
| `orders`        | Order lifecycle and delivery performance |
| `order_items`   | Product, price, and freight information  |
| `order_reviews` | Customer satisfaction                    |
| `products`      | Product characteristics                  |
| `customers`     | Geographic analysis                      |

This reduced the dataset to the information required for the analysis while keeping the analytical workflow focused and manageable.

### Data source

**Brazilian E-Commerce Public Dataset by Olist**

Available through Kaggle:

**[Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)**

---

## Data Architecture

The project begins by consolidating the selected source data into an analytical MySQL view:

```text
vw_olist_full
```

The analytical view combines the relevant information from the selected relational tables:

```text
orders
   │
   ├── order_items ─── products
   │
   ├── order_reviews
   │
   └── customers
```

This structure makes it possible to analyze logistics, products, customer satisfaction, and geography within a unified analytical dataset.

### Analytical Data Flow

```text
Olist Public Dataset
        │
        ▼
     MySQL
        │
        │  Data scoping
        │  Table selection
        │  SQL joins
        ▼
  vw_olist_full
        │
        ▼
SQLAlchemy + PyMySQL
        │
        ▼
vw_olist_full.csv
        │
        ▼
   Python / pandas
        │
        │  Data treatment
        │  Feature engineering
        │  KPI calculation
        │  Exploratory analysis
        ▼
Analytical CSV datasets
        │
        ▼
Microsoft Excel
        │
        ▼
Interactive Dashboards
```

---

## Data Preparation

After defining the analytical scope and creating the `vw_olist_full` view, the data was extracted from MySQL into Python.

The extraction workflow uses **SQLAlchemy** and **PyMySQL** to query the analytical view and create the dataset used in the subsequent analysis.

The main preparation steps included:

* Data cleaning;
* Variable renaming;
* Data type preparation;
* Creation of analytical variables;
* KPI calculation;
* Aggregation by seller;
* Aggregation by state;
* Comparison between delayed and on-time orders;
* Generation of analytical datasets for the dashboard.

---

## Feature Engineering

Several derived variables were created to support the analysis.

### Delivery Time

Measures the number of days between the order purchase and the actual customer delivery.

```text
delivery_time_days =
order_delivered_customer_date
-
order_purchase_timestamp
```

### Processing Time

Measures the number of days between purchase and order approval.

```text
processing_time_days =
order_approved_at
-
order_purchase_timestamp
```

### Late Delivery Flag

Identifies whether an order was delivered after the estimated delivery date.

```text
late_delivery_flag =
1 when actual delivery > estimated delivery
```

### Order-Level Metrics

Additional variables were created to support the analysis, including:

* Total order value;
* Number of items per order;
* Average item price;
* Average freight value;
* Monthly aggregation;
* Satisfaction level;
* Review comment indicator;
* Product volume;
* Geographic grouping.

---

## Key Metrics

The project uses operational and customer experience metrics to evaluate delivery performance.

### Delivery Delay Rate

Percentage of delivered orders that were delivered after the estimated delivery date.

### Average Delay

Average number of days of delay among delayed orders.

### Average Actual Delivery Time

Average number of days between purchase and actual delivery.

### Average Estimated Delivery Time

Average delivery time estimated for customers.

### Estimated vs. Actual Delivery Difference

Measures the difference between the estimated and actual delivery times, providing an indication of the accuracy of delivery expectations.

### Average Customer Score

Average review score associated with the analyzed orders.

### Probability of Rating 1

Probability that an order receives the lowest possible customer rating.

---

## Analysis & Dashboard

The final analysis is presented through three analytical sections in the Excel dashboard.

### 1. Logistics Performance

The logistics analysis focuses on seller-level delivery performance.

#### Top 10 Sellers by Delay Rate

Ranks sellers according to the percentage of their orders delivered late.

This metric identifies sellers where delivery problems occur most frequently.

#### Top 10 Sellers by Average Delay

Ranks sellers according to the average number of days of delay.

This metric measures the severity of delivery problems rather than their frequency.

Analyzing both metrics together is important because a seller can have:

* a high frequency of delays but relatively short delays; or
* a lower frequency of delays but significantly longer delays.

This distinction allows the analysis to identify different types of operational bottlenecks.

---

### 2. Delivery Delay & Customer Satisfaction

This section evaluates the relationship between delivery performance and customer experience.

#### Average Customer Score — Delayed vs. On-Time

Compares the average review score between orders delivered within the estimated timeframe and orders delivered late.

#### Probability of Rating 1 — Delayed vs. On-Time

Compares the probability of receiving the lowest possible rating in both scenarios.

This analysis provides a more direct measure of extreme customer dissatisfaction than the average score alone.

---

### 3. Geographic Performance

The geographic analysis evaluates delivery performance across Brazilian states.

#### Top 10 States by Delay Rate

Identifies the states where late deliveries occur most frequently.

#### Top 10 States by Average Delay

Identifies the states where delivery delays are longest.

These two metrics provide complementary views of regional performance:

> **Delay rate measures frequency, while average delay measures severity.**

---

## Key Findings

### Seller Performance

The seller analysis revealed substantial differences in delivery performance.

A group of sellers presented significantly higher delay rates and average delays than the rest of the analyzed marketplace.

This indicates that delivery problems are not evenly distributed across sellers and suggests opportunities for targeted operational intervention.

Rather than applying the same corrective action across the entire marketplace, sellers with consistently poor performance can be prioritized for monitoring and improvement plans.

---

### Geographic Performance

The analysis revealed distinct regional patterns in delivery performance.

States in the **Northeast**, including Alagoas (AL), Maranhão (MA), Sergipe (SE), and Piauí (PI), presented some of the highest delay rates.

At the same time, the highest average delays were concentrated primarily in **Northern states**, including Roraima (RR), Amapá (AP), and Amazonas (AM).

This indicates two different operational patterns:

* **Northeast:** higher frequency of delivery delays;
* **North:** longer delays when delivery problems occur.

The distinction is important because frequency and severity require different operational responses.

---

### Customer Satisfaction

The strongest finding of the analysis was the difference in customer satisfaction between delayed and on-time orders.

Orders delivered on time presented an average customer score of approximately:

**4.1 / 5**

while delayed orders presented an average score of approximately:

**2.5 / 5**

This represents an approximate **39% reduction in average customer rating** when comparing delayed orders with orders delivered on time.

The probability of receiving the lowest possible rating also increased substantially:

| Delivery status | Probability of rating 1 |
| --------------- | ----------------------: |
| On time         |                    ~10% |
| Delayed         |                    ~45% |

This means that delayed orders presented approximately a **4.5× higher probability of receiving a rating of 1**.

The result provides strong evidence that delivery performance is closely associated with customer satisfaction.

---

## Business Implications

The findings suggest that delivery performance should not be treated exclusively as an operational metric.

The relationship between delays and customer ratings indicates that logistics performance can directly influence the customer experience.

The main business implications are:

### Operational Efficiency

High delay rates may indicate bottlenecks in seller operations, order processing, transportation, or regional logistics.

### Customer Experience

Delayed orders are associated with significantly lower customer ratings and a substantially higher probability of extremely negative evaluations.

### Marketplace Reputation

A concentration of negative reviews associated with delivery problems can affect customer trust and the perceived reliability of the marketplace.

### Financial Impact

Although financial outcomes were not directly modeled in this project, persistent negative customer experiences may contribute indirectly to higher support costs, lower retention, and increased customer acquisition pressure.

---

## Recommendations

Based on the findings, the following actions are recommended.

### Prioritize Underperforming Sellers

Sellers with the highest delay rates and longest average delays should be prioritized for operational monitoring and corrective action.

### Establish Seller-Level Performance Monitoring

Delivery delay rate and average delay can be incorporated into recurring seller performance reviews.

### Develop Regional Logistics Strategies

The different patterns observed across Brazilian states suggest that logistics strategies should account for regional characteristics rather than applying a single approach to all locations.

### Improve Delivery Estimates

Estimated delivery dates should be continuously evaluated against actual performance to reduce the gap between customer expectations and operational reality.

### Proactively Communicate Delivery Risks

Orders identified as having a high probability of delay could trigger proactive communication with customers, potentially reducing frustration when delays cannot be completely avoided.

### Monitor Logistics and Customer Experience Together

Delivery KPIs should be analyzed alongside customer satisfaction metrics.

A logistics dashboard may identify an increase in delays, but customer experience metrics reveal the potential consequence of those delays.

---

## Project Structure

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

Contains the data extraction workflow and the analytical dataset exported from MySQL.

* `Extract.ipynb` — connects to MySQL and extracts the `vw_olist_full` analytical view using SQLAlchemy and PyMySQL.
* `vw_olist_full.csv` — exported analytical dataset used as the input for the Python analysis.

### `Projeto/`

Contains the main analysis, dashboard, and documentation.

* `Análise.ipynb` — performs data treatment, feature engineering, KPI calculation, and business analysis.
* `Dashboard.xlsx` — contains the interactive dashboards for logistics, customer satisfaction, and geographic performance.
* `Insights.MD` — documents the main findings, business implications, recommendations, and conclusions.

### `Tabelas/`

Contains the analytical datasets generated during the Python workflow.

* `atraso_vs_score.csv` — average customer score comparison between delayed and on-time orders.
* `atrasos_por_estado.csv` — delivery delay metrics aggregated by state.
* `atrasos_por_seller.csv` — delivery delay metrics aggregated by seller.
* `kpis_gerais.csv` — general logistics KPIs.
* `olist_tratada.csv` — treated analytical dataset.
* `probabilidade_nota1.csv` — probability of receiving rating 1 for delayed and on-time orders.

### `Mapa da base analítica Olist.txt`

Documents the analytical data model, selected source fields, relationships, and derived variables used throughout the project.

---

## Technologies

| Technology           | Purpose                                                                 |
| -------------------- | ----------------------------------------------------------------------- |
| **MySQL**            | Data scoping, relational data preparation, and analytical view creation |
| **SQL**              | Data selection, joins, filtering, and view construction                 |
| **Python**           | Data preparation, transformation, feature engineering, and analysis     |
| **pandas**           | Data manipulation and analytical processing                             |
| **SQLAlchemy**       | Database connection and data extraction                                 |
| **PyMySQL**          | MySQL connectivity                                                      |
| **Jupyter Notebook** | Extraction and analytical workflow                                      |
| **Microsoft Excel**  | Dashboard development and data visualization                            |

---

## Analytical Questions

The project was designed to answer the following business questions:

### Logistics Performance

* What percentage of orders were delivered late?
* What is the average delivery delay?
* Which sellers have the highest delay rates?
* Which sellers have the longest average delays?

### Geographic Performance

* Which states have the highest delay rates?
* Which states experience the longest delivery delays?
* Are delay patterns consistent across different regions?

### Customer Satisfaction

* How does the average customer rating differ between delayed and on-time orders?
* How does the probability of receiving a rating of 1 change when an order is delayed?
* How strongly are delivery delays associated with negative customer experiences?

---

## Data Source

The project uses the **Brazilian E-Commerce Public Dataset by Olist**, a publicly available dataset originally distributed through Kaggle.

**Source:**
[Brazilian E-Commerce Public Dataset by Olist — Kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)

The dataset is used for educational and portfolio purposes.

---

## AI-Assisted Development

The project was designed, developed, and analyzed by me, with AI used as a supporting tool during the development process.

AI assistance was used selectively for:

* SQL query review;
* Python code review;
* Technical discussions regarding relational data modeling;
* Data preparation and analysis best practices;
* Documentation review and organization.

The project scope, business questions, analytical methodology, metrics, interpretation of results, and final recommendations were defined as part of the project development process.

---

## Security

Database credentials were removed from the published project files.

No passwords, authentication credentials, or other sensitive connection information are included in the repository.

---

## Project Purpose

This project was developed as a portfolio case study to demonstrate practical capabilities across the data analytics workflow.

The project combines:

**Data Scoping → SQL → Data Extraction → Python → Feature Engineering → Exploratory Analysis → KPI Development → Business Intelligence → Business Insights**

The main objective was to demonstrate not only the ability to manipulate and visualize data, but also to transform a business problem into an analytical workflow and translate the resulting data into actionable conclusions.

---

## Conclusion

The analysis identified significant differences in delivery performance across sellers and Brazilian states and revealed a strong relationship between delivery delays and customer satisfaction.

Delayed orders presented substantially lower average customer ratings and a considerably higher probability of receiving the lowest possible rating.

The results reinforce the importance of treating logistics performance and customer experience as interconnected dimensions of e-commerce operations.

From an analytical perspective, the project demonstrates how a structured workflow can transform a large public dataset into a focused analytical solution capable of supporting decisions around seller performance, regional logistics, delivery estimates, and customer experience.


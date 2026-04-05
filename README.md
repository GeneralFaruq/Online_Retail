# Online Retail Data Analysis

## Why This Project Matters
Understanding customer behavior and sales performance is critical for any retail business.  
This project demonstrates how raw transactional data can be transformed into actionable insights using Python.

## Project Overview

This project explores transactional data from an online retail store to uncover insights into customer behavior, product performance, and sales trends.

Using Python, the analysis covers:

- Data cleaning and preprocessing
- Exploratory Data Analysis (EDA)
- Revenue and product insights
- Time-based sales trends
- Customer segmentation using RFM (Recency, Frequency, Monetary)

---

## Objectives

- Identify top-performing products and countries
- Analyze revenue trends over time
- Understand customer purchasing behavior
- Segment customers based on value and engagement

---

## Dataset Description

The dataset contains transactional records of an online retail store, including:

- InvoiceNo -> Unique transaction ID
- StockCode -> Product code
- Description -> Product name
- Quantity -> Number of items purchased
- InvoiceDate -> Date of transaction
- UnitPrice -> Price per unit
- CustomerID -> Unique customer identifier
- Country -> Customer location

---

## Data Cleaning Process

The dataset required several preprocessing steps:

- Removed rows with missing CustomerID
```python
df[df['CustomerID'].isnull()].head()
df = df.dropna(subset=['CustomerID'])  # removed rows with missing CustomerID
```

- Filtered out negative quantities (returns/cancellations)
```python
df = df[(df['Quantity'] > 0) & (df['UnitPrice'] > 0)] # Filter out rows with non-positive Quantity and UnitPrice
```

- Removed duplicate records
```python
df.duplicated().sum() # Check for duplicate rows
df = df.drop_duplicates() # Remove duplicate rows
df.duplicated().sum()
```

- Converted `InvoiceDate` to datetime format
```python
df['InvoiceDate'] = pd.to_datetime(df['InvoiceDate']) # Convert InvoiceDate to datetime format
```

- Created a new column:
  TotalPrice = Quantity × UnitPrice
```python
df['TotalPrice'] = df['Quantity'] * df['UnitPrice'] # Create a new column for total price
```
---

## Exploratory Data Analysis

### Top Products by Revenue
- Identified products generating the highest total revenue
- Helped highlight key revenue drivers
```python
top_products = df.groupby('Description')['TotalPrice'].sum().sort_values(ascending=False).head(10)
top_products.head(10)               # Display the top 10 products by total sales
Description
PAPER CRAFT , LITTLE BIRDIE           168469.60
REGENCY CAKESTAND 3 TIER              142264.75
WHITE HANGING HEART T-LIGHT HOLDER    100392.10
JUMBO BAG RED RETROSPOT                85040.54
MEDIUM CERAMIC TOP STORAGE JAR         81416.73
POSTAGE                                77803.96
PARTY BUNTING                          68785.23
ASSORTED COLOUR BIRD ORNAMENT          56413.03
Manual                                 53419.93
RABBIT NIGHT LIGHT                     51251.24
Name: TotalPrice, dtype: float64
```
### Revenue by Country

- Analyzed geographic distribution of sales
- Identified top-performing markets

---

## Time Series Analysis

### Monthly Revenue Trend

- Extracted year and month from transaction dates
- Observed how revenue changes over time
- Identified fluctuations and seasonal patterns

---

## Customer Analysis (RFM)

Customers were analyzed using three key metrics:

- Recency (R):
  How recently a customer made a purchase

- Frequency (F):
  How often a customer makes purchases

- Monetary (M):
  Total amount spent by the customer

### RFM Segmentation

Customers were grouped into segments such as:

- Best Customers
- Loyal Customers
- Recent Customers
- Others

This helps identify:

- High-value customers
- At-risk customers
- Engagement patterns

---

## Visualizations

The project includes both static and interactive visualizations using:

- Matplotlib
- Plotly (for interactive charts)

Examples:

- Top products bar charts
- Country revenue charts
- Monthly revenue trends
- Customer segment distributions

---

## Key Insights

- A small number of products generate a large portion of revenue
- Revenue shows fluctuations over time (possible seasonality)
- Most customers purchase infrequently
- A small group of customers contributes the majority of revenue
- High-value customers can be targeted for retention strategies

---

## Conclusion

This analysis demonstrates how transactional data can be transformed into actionable business insights.

---

## Tools & Technologies

* Python
* Pandas
* Matplotlib
* Plotly
* Jupyter Notebook (VS Code)

---

## Project Structure

```
├── Online_Retail.ipynb
├── Online_Retail.csv
└── README.md
```
---

## Acknowledgment

This project is part of a data analysis learning journey focused on building real-world analytical skills.

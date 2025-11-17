# Customer Segmentation For Marketing Campaigns in SuperStore (Global Retail Company) | Python
<img width="900" height="600" alt="Image" src="https://github.com/user-attachments/assets/f26fd9d1-2d88-4dec-a650-d558bae94f47" />

*Applying the RFM model built with Python to segment customers and recommend appropriate marketing campaigns.*

**Author:** Nguyễn Duy Kiên

**Date:** October 2025

**Tools Used:** Python

---

## 📑 Table of Contents  
1. [📌 Background & Overview](#1--background--overview)  
2. [📂 Dataset Description & Data Structure](#2--dataset-description--data-structure)
3. [🔍 Exploratory Data Analysis (EDA)](3--exploratory-data-analysis-eda)
4. [🧮 Data Processing](4--data-processing)
5. [📊 Visulization & Analysis](5--visulization--analysis)
6. [🔎 Insights & Recommendations](6--insights--recommendations)

---

## 1. 📌 Background & Overview 

### 1.1. Objective:
### 📖 What is this project about? What Business Question will it solve?

🎯 Main Business Question

How can SuperStore use RFM segmentation to efficiently categorize customers and design high-impact marketing campaigns for Christmas and New Year?

📘 Project Overview

- This project applies the RFM (Recency – Frequency – Monetary) model to segment customers based on their purchase behavior.
- The goal is to analyze customer value and classify customers into actionable segments for marketing campaigns.
- The dataset comes from SuperStore, a global retail company with a large customer base.
- Because of the large volume of data, the segmentation is implemented with Python, replacing the manual Excel method previously used.
- The analysis includes:
    + Preparing RFM-ready dataset
    + Calculating R, F, M scores (using 31/12/2011 as the reference date for Recency)
    + Applying quintile scoring (1–5 scale)
    + Assigning segments
    + Visualizing segment distributions
    + Giving insights and marketing recommendations

💡 Business Questions this project answers

- ✔️ How can SuperStore segment its entire customer base using RFM to support targeted marketing?
- ✔️ Which customer groups have high value (loyal, big spenders) and which groups have churn risk?
- ✔️ How should Marketing tailor campaigns for each segment to maximize retention, loyalty, and sales uplift?
- ✔️ What is the current distribution of customer value across Recency, Frequency, and Monetary?
- ✔️ Which RFM dimension is most critical for SuperStore’s retail business model?

### 1.2. Who is this project for?  

- ✔️ Marketing Department – to personalize campaigns, allocate budgets, and target high-value or at-risk customers.
- ✔️ Sales Teams – to identify loyal customers and upsell/cross-sell opportunities.
- ✔️ Customer Experience / CRM Teams – to tailor retention and reactivation programs.
- ✔️ Data Analytics Department – to automate segmentation pipelines and maintain scalable customer analytics.
- ✔️ Business Leaders / Executives – to understand customer value distribution and guide strategic planning.

### 1.3. Why RFM? How to apply RFM?

🚩 Why RFM?

RFM is a marketing method that looks at three things: Recency, Frequency, and Monetary value.
- Recency: How long it has been since a customer last bought something.
- Frequency: How many times the customer has made purchases.
- Monetary: How much money the customer has spent in total.

This method helps businesses group and understand their customers based on how recently they buy, how often they buy, and how much they spend. RFM is especially useful for small and medium businesses because it helps them target the right customer groups, increase ROI, lower churn, save marketing cost, and improve customer relationships.

🚩 How does it work?
- In RFM analysis, each customer is given a score for Recency, Frequency, and Monetary value. To do this, the data is usually split into five groups (quintiles) for each factor. 
- After scoring all three metrics using these quintiles, customers are then grouped into segments based on the combination of their R, F, and M scores. This helps businesses easily identify high-value customers, loyal customers, or customers at risk of leaving.

---

## 2. 📂 Dataset Description & Data Structure

### 2.1. Tables Used

The dataset consists of two tables (sheets):
- Sheet 1: E-commerce Retail – Contains transaction-level data, including order details, customer IDs, and purchase information.

|        | InvoiceNo | StockCode |                         Description | Quantity |         InvoiceDate | UnitPrice | CustomerID |        Country |
|--------|-----------|-----------|-------------------------------------|----------|---------------------|-----------|------------|----------------|
|    0   |    536365 |    85123A |  WHITE HANGING HEART T-LIGHT HOLDER |        6 | 2010-12-01 08:26:00 |      2.55 |    17850.0 | United Kingdom |
|    1   |    536365 |     71053 |                 WHITE METAL LANTERN |        6 | 2010-12-01 08:26:00 |      3.39 |    17850.0 | United Kingdom |
|    2   |    536365 |    84406B |      CREAM CUPID HEARTS COAT HANGER |        8 | 2010-12-01 08:26:00 |      2.75 |    17850.0 | United Kingdom |
|    3   |    536365 |    84029G | KNITTED UNION FLAG HOT WATER BOTTLE |        6 | 2010-12-01 08:26:00 |      3.39 |    17850.0 | United Kingdom |
|    4   |    536365 |    84029E |      RED WOOLLY HOTTIE WHITE HEART. |        6 | 2010-12-01 08:26:00 |      3.39 |    17850.0 | United Kingdom |
|   ...  |       ... |       ... |                                 ... |      ... |                 ... |       ... |        ... |            ... |
| 541904 |    581587 |     22613 |         PACK OF 20 SPACEBOY NAPKINS |       12 | 2011-12-09 12:50:00 |      0.85 |    12680.0 |         France |
| 541905 |    581587 |     22899 |         CHILDREN'S APRON DOLLY GIRL |        6 | 2011-12-09 12:50:00 |      2.10 |    12680.0 |         France |
| 541906 |    581587 |     23254 |        CHILDRENS CUTLERY DOLLY GIRL |        4 | 2011-12-09 12:50:00 |      4.15 |    12680.0 |         France |
| 541907 |    581587 |     23255 |     CHILDRENS CUTLERY CIRCUS PARADE |        4 | 2011-12-09 12:50:00 |      4.15 |    12680.0 |         France |
| 541908 |    581587 |     22138 |        BAKING SET 9 PIECE RETROSPOT |        3 | 2011-12-09 12:50:00 |      4.95 |    12680.0 |         France |

- Sheet 2: Segmentation – Stores customer segments along with their RFM scores.

|        Segment        |                                                        RFM Score                                                       |
|-----------------------|------------------------------------------------------------------------------------------------------------------------|
| Champions             | 555, 554, 544, 545, 454, 455, 445                                                                                      |
| Loyal                 | 543, 444, 435, 355, 354, 345, 344, 335                                                                                 |
| Potential Loyalist    | 553, 551, 552, 541, 542, 533, 532, 531, 452, 451, 442, 441, 431, 453, 433, 432, 423, 353, 352, 351, 342, 341, 333, 323 |
| New Customers         | 512, 511, 422, 421, 412, 411, 311                                                                                      |
| Promising             | 525, 524, 523, 522, 521, 515, 514, 513, 425, 424, 413, 414, 415, 315, 314, 313                                         |
| Need Attention        | 535, 534, 443, 434, 343, 334, 325, 324                                                                                 |
| About To Sleep        | 331, 321, 312, 221, 213, 231, 241, 251                                                                                 |
| At Risk               | 255, 254, 245, 244, 253, 252, 243, 242, 235, 234, 225, 224, 153, 152, 145, 143, 142, 135, 134, 133, 125, 124           |
| Cannot Lose Them      | 155, 154, 144, 214, 215, 115, 114, 113                                                                                 |
| Hibernating Customers | 332, 322, 233, 232, 223, 222, 132, 123, 122, 212, 211                                                                  |
| Lost Customers        | 111, 112, 121, 131, 141, 151                                                                                           |

### 2.2. Table Schema & Data Snapshot

📌 Sheet 1: E-commerce Retail

| Column Name |    Data Type   |                                                Description                                                |
|-------------|----------------|-----------------------------------------------------------------------------------------------------------|
| InvoiceNo   | object         | Unique invoice number for each transaction (6-digit). If it starts with 'C', it indicates a cancellation. |
| StockCode   | object         | Unique product (item) code (5-digit).                                                                     |
| Description | object         | Product (item) name.                                                                                      |
| Quantity    | int64          | The number of units purchased per transaction.                                                            |
| InvoiceDate | datetime64[ns] | Date and time when the transaction occurred.                                                              |
| UnitPrice   | float64        | Price per unit of the product in sterling.                                                                |
| CustomerID  | float64        | Unique 5-digit identifier for each customer.                                                              |
| Country     | object         | Name of the country where the customer resides.                                                           |

📌 Sheet 2: Segmentation

| Column Name |          Description          |
|:------------|:------------------------------|
| Segment     | Segment Name                  |
| RFM Score   | List of score in that Segment |

## 3. 🔍 Exploratory Data Analysis (EDA)

### 3.1. Understand Data

#### a. Import Packages & Load Data Set

```python
%%capture
! pip install pandas-profiling
! pip install pydantic-settings
! pip install ydata_profiling
! pip install squarify

import pandas as pd
from pandas_profiling import ProfileReport
from ydata_profiling import ProfileReport
import seaborn as sns
import numpy as np

import matplotlib.pyplot as plt
import squarify

df = pd.read_excel("/content/drive/MyDrive/Final_project_RFM/ecommerce retail.xlsx",sheet_name = "ecommerce retail")
df.head()
```
|   | InvoiceNo | StockCode |                         Description | Quantity |         InvoiceDate | UnitPrice | CustomerID |        Country |
|--:|----------:|----------:|------------------------------------:|---------:|--------------------:|----------:|-----------:|---------------:|
| 0 |    536365 |    85123A |  WHITE HANGING HEART T-LIGHT HOLDER |        6 | 2010-12-01 08:26:00 |      2.55 |    17850.0 | United Kingdom |
| 1 |    536365 |     71053 |                 WHITE METAL LANTERN |        6 | 2010-12-01 08:26:00 |      3.39 |    17850.0 | United Kingdom |
| 2 |    536365 |    84406B |      CREAM CUPID HEARTS COAT HANGER |        8 | 2010-12-01 08:26:00 |      2.75 |    17850.0 | United Kingdom |
| 3 |    536365 |    84029G | KNITTED UNION FLAG HOT WATER BOTTLE |        6 | 2010-12-01 08:26:00 |      3.39 |    17850.0 | United Kingdom |
| 4 |    536365 |    84029E |      RED WOOLLY HOTTIE WHITE HEART. |        6 | 2010-12-01 08:26:00 |      3.39 |    17850.0 | United Kingdom |

#### b. Data Type & Data Value

```python
# information of the table to detect the data type of each column
print(df.info())

print('')

# help detect the data value of the columns (min, max, count,...)
print(df.describe())
```

| # | Column      | Non-Null Count  | Dtype          |
|---|-------------|-----------------|----------------|
| 0 | InvoiceNo   | 541909 non-null | object         |
| 1 | StockCode   | 541909 non-null | object         |
| 2 | Description | 540455 non-null | object         |
| 3 | Quantity    | 541909 non-null | int64          |
| 4 | InvoiceDate | 541909 non-null | datetime64[ns] |
| 5 | UnitPrice   | 541909 non-null | float64        |
| 6 | CustomerID  | 406829 non-null | float64        |
| 7 | Country     | 541909 non-null | object         |

|       | Quantity      | InvoiceDate                   | UnitPrice     | CustomerID    |
|-------|---------------|-------------------------------|---------------|---------------|
| count | 541909.000000 | 541909                        | 541909.000000 | 406829.000000 |
| mean  | 9.552250      | 2011-07-04 13:34:57.156386048 | 4.611114      | 15287.690570  |
| min   | -80995.000000 | 2010-12-01 08:26:00           | -11062.060000 | 12346.000000  |
| 25%   | 1.000000      | 2011-03-28 11:34:00           | 1.250000      | 13953.000000  |
| 50%   | 3.000000      | 2011-07-19 17:17:00           | 2.080000      | 15152.000000  |
| 75%   | 10.000000     | 2011-10-19 11:27:00           | 4.130000      | 16791.000000  |
| max   | 80995.000000  | 2011-12-09 12:50:00           | 38970.000000  | 18287.000000  |
| std   | 218.081158    | NaN                           | 96.759853     | 1713.600303   |

#### c. Using ProfileReport to Understand more about Category Data Type

```python
# @title c. Using ProfileReport to Understand more about Category Data Type
profile = ProfileReport(df)
profile
```

<img width="1936" height="706" alt="Image" src="https://github.com/user-attachments/assets/d057fc39-c0ea-42b8-8d37-719e44f17d83" />

<img width="1935" height="663" alt="image" src="https://github.com/user-attachments/assets/eea1a117-e952-4c93-a864-d91a170487bf" />

#### d. Detect the reason for the unreasonable column data value (Quantity < 0)

```python
# quick check why data Quantity < 0
print('Print top 5 rows with values ​​having Quantity < 0')
print(df[df.Quantity < 0].head())
print('')

# continue to check if the reason for the Quantity < 0 column is due to a canceled transaction
print('Check if the reason for the Quantity < 0 column is due to a canceled transaction')
df['InvoiceNo'] = df['InvoiceNo'].astype(str)
df['check_cancel'] = df['InvoiceNo'].apply(lambda x: True if x[0] == 'C' else False)
print(df[(df.Quantity < 0) & (df.check_cancel == True)].head())

print('')
df[(df.Quantity < 0) & (df.check_cancel == False)].head()
```
<img width="1460" height="1085" alt="image" src="https://github.com/user-attachments/assets/aee6472e-9a2d-4f50-8675-4ff2f2f60aa9" />

#### e. Detect the reason for the unreasonable data value column (Price < 0)

```python
# quick check why Unit Price < 0
print('Print some values ​​with UnitPrice < 0')
df[df.UnitPrice < 0].head()
```
|        | InvoiceNo | StockCode |     Description | Quantity |         InvoiceDate | UnitPrice | CustomerID |        Country | check_cancel |
|--------|----------:|----------:|----------------:|---------:|--------------------:|----------:|-----------:|---------------:|-------------:|
| 299983 |   A563186 |         B | Adjust bad debt |        1 | 2011-08-12 14:51:00 | -11062.06 |        NaN | United Kingdom |        False |
| 299984 |   A563187 |         B | Adjust bad debt |        1 | 2011-08-12 14:52:00 | -11062.06 |        NaN | United Kingdom |        False |

#### f. Insights:

⚡ Initial Data Quality Findings

Early exploration revealed that both the Quantity and Unit Price columns contain negative values, which are not logically valid. These issues require deeper investigation. Potential next steps include:

- Verifying whether values were incorrectly entered.

- Checking if negatives represent refunds or cancellations.

- Cleaning, correcting, or excluding invalid records to maintain analytical accuracy.

⚡ Data Consistency Issues

A discrepancy was found between the number of StockCode entries (4070) and Description entries (4223). This indicates possible data quality problems. Potential causes include:

- One stock code corresponding to multiple descriptions.

- Descriptions not linked to valid stock codes.

- Missing, duplicated, or improperly recorded product information.

A thorough validation and cleaning process is recommended to ensure dataset reliability.

⚡ Required Manual Review

Certain orders appear to have incorrect product descriptions. These entries should be manually reviewed and labeled as errors for follow-up processing.

⚡ Invalid Transaction Identification
After filtering cancellations, ensure there are no cases where Quantity < 0 but InvoiceNo does NOT start with “C”, as these reflect inconsistencies that must be addressed.

✨ Conclusion

- Incorrect Data Types: Columns such as InvoiceNo, StockCode, Description, CustomerID, and Country should be converted to string format for proper handling.

- Data Value Rules:

    + Quantity < 0 and InvoiceNo starts with “C” → Valid cancellations → Should be removed from the analysis.

    + Quantity < 0 but InvoiceNo does NOT start with “C” → Incorrect records → Should be excluded.

    + UnitPrice < 0 combined with incorrect descriptions → Invalid transactions → Must be removed.

### 3.2. Handling invalid data types and values

```python
# convert data fields to the correct format
print(df.columns)
print('')

column_list = ['InvoiceNo','StockCode','Description','CustomerID','Country']
for c in column_list:
df[c] = df[c].astype(str)

# drop data value is not suitable
## drop data value with UnitPrice < 0
df = df[df['UnitPrice'] > 0]
## drop data with Quantity < 0
df = df[df['Quantity'] > 0]
## drop data is Canceled
df = df[df.check_cancel == False]
df = df.replace('nan', None)
df = df.replace('Nan',None)
df.shape
```

### 3.3. Handle Missing Values

#### a. Count columns with missing values

```python
# check missing value in data
print('Statistics on columns with missing values')
missing_dict = { 
'volume': df.isnull().sum(), 
'percent': df.isnull().sum() / (df.shape[0])}

missing_df = pd.DataFrame.from_dict(missing_dict)
missing_df.head(10)
```

|              | volume | percent  |
|--------------|--------|----------|
| InvoiceNo    | 0      | 0.000000 |
| StockCode    | 0      | 0.000000 |
| Description  | 0      | 0.000000 |
| Quantity     | 0      | 0.000000 |
| InvoiceDate  | 0      | 0.000000 |
| UnitPrice    | 0      | 0.000000 |
| CustomerID   | 132220 | 0.249423 |
| Country      | 0      | 0.000000 |
| check_cancel | 0      | 0.000000 |

#### b. Check the reason why some data is missing a lot
```python
# check why CustomerID is null so often
print(df[df.CustomerID.isnull()].head())

print('')

print(df[df.CustomerID.isnull()].tail())

# check null distribution over time
df['Day'] = pd.to_datetime(df['InvoiceDate']).dt.date
df['Month'] = df['Day'].apply(lambda x: str(x)[:-3])

df_group_day = df[df.CustomerID.isnull()][['Month','InvoiceNo']].groupby(['Month']).count().reset_index().sort_values(by = ['Month'], ascending = True)
df_group_day.head(50)
```

<img width="900" height="1262" alt="image" src="https://github.com/user-attachments/assets/fa1c2bc8-4546-45f1-8575-472d9ea66aab" />

#### c. Insights

General comments:
- A huge number of missing in every month -> Missing is not a small error. It is a systematic missing.
- Invoices with CustomerID = NULL are transactions without customer registration (guest checkout) -> usually walk-in customers or direct retail at the store.
- If these Null lines are left, RFM cannot be calculated.
- 
Solution:
- Drop all Nulls.

#### d. Handle Mising Value

```python
# handle missing values
## drop 20% of missing users
df = df[df['CustomerID'].notnull()]
```

### 3.4. Handle Duplicates

#### a. List columns with Duplicates

```python
# check duplicated values ​​in dataset
## What is duplicate data
#df_description_update.head()
df_duplication = df.duplicated(subset=["InvoiceNo", "StockCode","InvoiceDate","CustomerID"])
print (df[df_duplication].shape)
print('')
print(df.shape)
```

<img width="1040" height="436" alt="image" src="https://github.com/user-attachments/assets/141dbffb-0691-47e5-80cb-008305e04346" />


#### b. Reason for duplicate

```python
# What is the reason for duplication
print(df[df_duplication].head())

print('')

print(df[(df.InvoiceNo == '536381') & (df.StockCode == 71270)].head())

print('')

print(df[(df.InvoiceNo == '536401') & (df.StockCode == 82580)].head())
```
<img width="1829" height="881" alt="image" src="https://github.com/user-attachments/assets/95dd0a42-1fa2-476d-a9cd-194430a3c726" />

#### c. Insights

General comments:
- Duplicate in this dataset is a record that is recorded multiple times exactly because of a system error. It makes the revenue wrong, RFM wrong.
- So duplicate in this dataset is not the same invoice with many lines (that is normal because 1 invoice has many products) and not the same invoice + same stock but different quantity (that is a sale update — not duplicate)

Solution: Drop all

#### d. Handle Duplicates

```python
# drop duplications
df_drop_duplications = df.drop_duplicates(subset=["InvoiceNo", "StockCode","InvoiceDate","CustomerID"], keep = 'first')
df_drop_duplications.shape
```

<img width="973" height="216" alt="image" src="https://github.com/user-attachments/assets/1de60774-6689-4f72-ba1a-ae9b6159565c" />

```python
df_drop_duplications.head()
```

|   | InvoiceNo | StockCode | Description                         | Quantity | InvoiceDate         | UnitPrice | CustomerID | Country        | check_cancel | Day        | Month   |
|---|-----------|-----------|-------------------------------------|----------|---------------------|-----------|------------|----------------|--------------|------------|---------|
| 0 | 536365    | 85123A    | WHITE HANGING HEART T-LIGHT HOLDER  | 6        | 2010-12-01 08:26:00 | 2.55      | 17850.0    | United Kingdom | False        | 2010-12-01 | 2010-12 |
| 1 | 536365    | 71053     | WHITE METAL LANTERN                 | 6        | 2010-12-01 08:26:00 | 3.39      | 17850.0    | United Kingdom | False        | 2010-12-01 | 2010-12 |
| 2 | 536365    | 84406B    | CREAM CUPID HEARTS COAT HANGER      | 8        | 2010-12-01 08:26:00 | 2.75      | 17850.0    | United Kingdom | False        | 2010-12-01 | 2010-12 |
| 3 | 536365    | 84029G    | KNITTED UNION FLAG HOT WATER BOTTLE | 6        | 2010-12-01 08:26:00 | 3.39      | 17850.0    | United Kingdom | False        | 2010-12-01 | 2010-12 |
| 4 | 536365    | 84029E    | RED WOOLLY HOTTIE WHITE HEART.      | 6        | 2010-12-01 08:26:00 | 3.39      | 17850.0    | United Kingdom | False        | 2010-12-01 | 2010-12 |

## 4. 🧮 Data Processing

### 4.1. RFM Model

#### a. Add more information to process

```python
%%capture
df_drop_duplications['cost'] = df_drop_duplications['Quantity'] *  df_drop_duplications['UnitPrice']
last_day = df_drop_duplications['Day'].max()

RFM_df = df_drop_duplications.groupby('CustomerID').agg(
    Recency = ('Day', lambda x: last_day - x.max()),
    Frequency = ('CustomerID','count'),
    Monetary = ('cost','sum'),
    Start_Day = ('Day', 'min')).reset_index()

RFM_df['Recency'] = RFM_df['Recency'].dt.days.astype('int16')
RFM_df['Recency_reverse'] = - RFM_df['Recency'] 
RFM_df['Start_Day'] = pd.to_datetime(RFM_df['Start_Day'])
RFM_df['Start_Month'] = RFM_df['Start_Day'].apply(lambda x : x.replace(day=1))
```

#### b. Use qcut to create R, F, M

```python
RFM_df['R'] = pd.qcut(RFM_df["Recency_reverse"], 5, labels = range(1, 6)).astype(str) # Score recency
RFM_df['F'] = pd.qcut(RFM_df["Frequency"], 5, labels = range(1, 6)).astype(str)
RFM_df['M'] = pd.qcut(RFM_df["Monetary"], 5, labels = range(1, 6)).astype(str)
RFM_df['RFM'] = RFM_df.apply(lambda x: x.R + x.F + x.M, axis = 1)
RFM_df.head()
```
|   | CustomerID | Recency | Frequency | Monetary | Start_Day  | Recency_reverse | Start_Month | R | F | M | RFM |
|---|------------|---------|-----------|----------|------------|-----------------|-------------|---|---|---|-----|
| 0 | 12346.0    | 325     | 1         | 77183.60 | 2011-01-18 | -325            | 2011-01-01  | 1 | 1 | 5 | 115 |
| 1 | 12347.0    | 2       | 182       | 4310.00  | 2010-12-07 | -2              | 2010-12-01  | 5 | 5 | 5 | 555 |
| 2 | 12348.0    | 75      | 27        | 1595.64  | 2010-12-16 | -75             | 2010-12-01  | 2 | 2 | 4 | 224 |
| 3 | 12349.0    | 18      | 73        | 1757.55  | 2011-11-21 | -18             | 2011-11-01  | 4 | 4 | 4 | 444 |
| 4 | 12350.0    | 310     | 17        | 334.40   | 2011-02-02 | -310            | 2011-02-01  | 1 | 2 | 2 | 122 |

#### c. Merge with Segmentation explanation

```python
#Import Segment Explaination
seg = pd.read_excel("/content/drive/MyDrive/Final_project_RFM/ecommerce retail.xlsx",sheet_name = "Segmentation")
seg['RFM Score'] = seg['RFM Score'].str.split(',')
seg = seg.explode('RFM Score').reset_index(drop = True)

#Remove extra spaces
seg['RFM Score'] = seg['RFM Score'].apply(lambda x: x.strip())

#Merge
RFM_df_final = RFM_df.merge(seg, how = 'left', left_on = 'RFM', right_on = 'RFM Score')
RFM_df_final.head()
```

|   | CustomerID | Recency | Frequency | Monetary | Start_Day  | Recency_reverse | Start_Month | R | F | M | RFM | Segment               | RFM Score |
|---|------------|---------|-----------|----------|------------|-----------------|-------------|---|---|---|-----|-----------------------|-----------|
| 0 | 12346.0    | 325     | 1         | 77183.60 | 2011-01-18 | -325            | 2011-01-01  | 1 | 1 | 5 | 115 | Cannot Lose Them      | 115       |
| 1 | 12347.0    | 2       | 182       | 4310.00  | 2010-12-07 | -2              | 2010-12-01  | 5 | 5 | 5 | 555 | Champions             | 555       |
| 2 | 12348.0    | 75      | 27        | 1595.64  | 2010-12-16 | -75             | 2010-12-01  | 2 | 2 | 4 | 224 | At Risk               | 224       |
| 3 | 12349.0    | 18      | 73        | 1757.55  | 2011-11-21 | -18             | 2011-11-01  | 4 | 4 | 4 | 444 | Loyal                 | 444       |
| 4 | 12350.0    | 310     | 17        | 334.40   | 2011-02-02 | -310            | 2011-02-01  | 1 | 2 | 2 | 122 | Hibernating customers | 122       |

### 4.2. Variables Loyal customer, Non-loyal customer, Customer characteristics - Predicting potential Loyal Customer

#### a. Average order value, average order volume

```python
# Loyal status
RFM_df_final['loyal_status'] = RFM_df_final['Segment'].apply(lambda x: 'Loyal' if x in ('Loyal','Potential Loyalist') else 'Non Loyal')

## Average order value, average order volume
RFM_df_average = df_drop_duplications.groupby('CustomerID').agg(
    Quantity_average=('Quantity', 'mean'),
    Cost_average=('cost', 'mean'),
).reset_index()
RFM_df_average.head()
```

|   | CustomerID | Quantity_average | Cost_average |
|---|------------|------------------|--------------|
| 0 | 12346.0    | 74215.000000     | 77183.600000 |
| 1 | 12347.0    | 13.505495        | 23.681319    |
| 2 | 12348.0    | 68.925926        | 59.097778    |
| 3 | 12349.0    | 8.643836         | 24.076027    |
| 4 | 12350.0    | 11.588235        | 19.670588    |

#### b. First order value, first order quantity

```python
### rn (row number) column to find the first order
df_drop_duplications['rn'] = df_drop_duplications.groupby(['CustomerID'])['InvoiceDate'].rank(method = 'first')
RFM_df_first = df_drop_duplications[df_drop_duplications.rn == 1][['CustomerID','Quantity','cost']].rename(columns = {'Quantity':'First Quantiy','cost':'First cost'})
RFM_df_first.head()
```

|    | CustomerID | First Quantiy | First cost |
|----|------------|---------------|------------|
| 0  | 17850.0    | 6             | 15.30      |
| 9  | 13047.0    | 32            | 54.08      |
| 26 | 12583.0    | 24            | 90.00      |
| 46 | 13748.0    | 80            | 204.00     |
| 65 | 15100.0    | 32            | 350.40     |

#### c. Merge with RFM table

```python
RFM_df_final = RFM_df_final.merge(RFM_df_average, how = 'left', on = 'CustomerID')
RFM_df_final = RFM_df_final.merge(RFM_df_first, how = 'left', on = 'CustomerID')
RFM_df_final.head()
```

|   | CustomerID | Recency | Frequency | Monetary | Start_Day  | Recency_reverse | Start_Month | R | F | M | RFM | Segment               | RFM Score | loyal_status | Quantity_average | Cost_average | First Quantiy | First cost |
|---|------------|---------|-----------|----------|------------|-----------------|-------------|---|---|---|-----|-----------------------|-----------|--------------|------------------|--------------|---------------|------------|
| 0 | 12346.0    | 325     | 1         | 77183.60 | 2011-01-18 | -325            | 2011-01-01  | 1 | 1 | 5 | 115 | Cannot Lose Them      | 115       | Non Loyal    | 74215.000000     | 77183.600000 | 74215         | 77183.6    |
| 1 | 12347.0    | 2       | 182       | 4310.00  | 2010-12-07 | -2              | 2010-12-01  | 5 | 5 | 5 | 555 | Champions             | 555       | Non Loyal    | 13.505495        | 23.681319    | 12            | 25.2       |
| 2 | 12348.0    | 75      | 27        | 1595.64  | 2010-12-16 | -75             | 2010-12-01  | 2 | 2 | 4 | 224 | At Risk               | 224       | Non Loyal    | 68.925926        | 59.097778    | 72            | 39.6       |
| 3 | 12349.0    | 18      | 73        | 1757.55  | 2011-11-21 | -18             | 2011-11-01  | 4 | 4 | 4 | 444 | Loyal                 | 444       | Loyal        | 8.643836         | 24.076027    | 2             | 15.0       |
| 4 | 12350.0    | 310     | 17        | 334.40   | 2011-02-02 | -310            | 2011-02-01  | 1 | 2 | 2 | 122 | Hibernating customers | 122       | Non Loyal    | 11.588235        | 19.670588    | 12            | 25.2       |

#### d. Sort bins for Quantity Average, Cost Average, First Quality, First cost

```python
# Function to calculate percentile thresholds
def percentile_threshold(column):
    p_25 = column.quantile(0.25)
    p_50 = column.quantile(0.5)
    p_75 = column.quantile(0.75)
    quantile_list = [p_25, p_50, p_75]
    return quantile_list

# Function to assign quantile thresholds
def quantile_threshold(x, quantile_list):
    if x <= quantile_list[0]:
        value = f'q1: < {round(quantile_list[0])}'  # Format as string with 2 decimal places
    elif x <= quantile_list[1]:
        value = f'q2: {round(quantile_list[0])} - {round(quantile_list[1])}'
    elif x <= quantile_list[2]:
        value = f'q3: {round(quantile_list[1])} - {round(quantile_list[2])}'
    else:
        value = f'q4: > {round(quantile_list[2])}'
    return value

# Apply thresholds and assign bins for Quantity average
quantity_average_list = percentile_threshold(RFM_df_final['Quantity_average'])
RFM_df_final['Quantity_average_bin'] = RFM_df_final['Quantity_average'].apply(
    lambda x: quantile_threshold(x, quantity_average_list)
)

# Apply thresholds and assign bins for Cost average
cost_average_list = percentile_threshold(RFM_df_final['Cost_average'])
RFM_df_final['Cost_average_bin'] = RFM_df_final['Cost_average'].apply(
    lambda x: quantile_threshold(x, cost_average_list)
)

# Apply thresholds and assign bins for First Quantity
first_quantity_list = percentile_threshold(RFM_df_final['First Quantiy'])
RFM_df_final['First Quantity bin'] = RFM_df_final['First Quantiy'].apply(
    lambda x: quantile_threshold(x, first_quantity_list)
)

# Apply thresholds and assign bins for First Cost
first_cost_list = percentile_threshold(RFM_df_final['First cost'])
RFM_df_final['First cost bin'] = RFM_df_final['First cost'].apply(
    lambda x: quantile_threshold(x, first_cost_list)
)

# Display the updated DataFrame
RFM_df_final.head()
```

|   | CustomerID | Recency | Frequency | Monetary | Start_Day  | Recency_reverse | Start_Month | R | F | M | ... | RFM Score | loyal_status | Quantity_average | Cost_average | First Quantiy | First cost | Quantity_average_bin | Cost_average_bin | First Quantity bin | First cost bin |
|---|------------|---------|-----------|----------|------------|-----------------|-------------|---|---|---|-----|-----------|--------------|------------------|--------------|---------------|------------|----------------------|------------------|--------------------|----------------|
| 0 | 12346.0    | 325     | 1         | 77183.60 | 2011-01-18 | -325            | 2011-01-01  | 1 | 1 | 5 | ... | 115       | Non Loyal    | 74215.000000     | 77183.600000 | 74215         | 77183.6    | q4: > 15             | q4: > 25         | q4: > 12           | q4: > 26       |
| 1 | 12347.0    | 2       | 182       | 4310.00  | 2010-12-07 | -2              | 2010-12-01  | 5 | 5 | 5 | ... | 555       | Non Loyal    | 13.505495        | 23.681319    | 12            | 25.2       | q3: 10 - 15          | q3: 18 - 25      | q3: 8 - 12         | q3: 16 - 26    |
| 2 | 12348.0    | 75      | 27        | 1595.64  | 2010-12-16 | -75             | 2010-12-01  | 2 | 2 | 4 | ... | 224       | Non Loyal    | 68.925926        | 59.097778    | 72            | 39.6       | q4: > 15             | q4: > 25         | q4: > 12           | q4: > 26       |
| 3 | 12349.0    | 18      | 73        | 1757.55  | 2011-11-21 | -18             | 2011-11-01  | 4 | 4 | 4 | ... | 444       | Loyal        | 8.643836         | 24.076027    | 2             | 15.0       | q2: 6 - 10           | q3: 18 - 25      | q1: < 3            | q2: 10 - 16    |
| 4 | 12350.0    | 310     | 17        | 334.40   | 2011-02-02 | -310            | 2011-02-01  | 1 | 2 | 2 | ... | 122       | Non Loyal    | 11.588235        | 19.670588    | 12            | 25.2       | q3: 10 - 15          | q3: 18 - 25      | q3: 8 - 12         | q3: 16 - 26    |

## 5. 📊 Visulization & Analysis

### 5.1. RFM Model

```python
# Distribution (number of Customers, revenue) by Segment. From there, detect the majority of Customer groups and have appropriate Marketing strategies.
# Set the figure size
segment_by_user_count = RFM_df_final[['Segment','CustomerID']].groupby(['Segment']).count().reset_index().rename(columns = {'CustomerID':'user_volume'})
segment_by_user_count['contribution_percent'] = round(segment_by_user_count['user_volume'] / segment_by_user_count['user_volume'].sum() * 100)
segment_by_user_count['type'] = 'User contribution'

segment_by_spending = RFM_df_final[['Segment','Monetary']].groupby(['Segment']).sum().reset_index().rename(columns = {'Monetary':'spending'})
segment_by_spending['contribution_percent'] = segment_by_spending['spending'] / segment_by_spending['spending'].sum() * 100
segment_by_spending['type'] = 'Spending contribution'

segment_agg = pd.concat([segment_by_user_count, segment_by_spending])

plt.figure(figsize=(21, 8))
sns.barplot(segment_agg, x="Segment", y="contribution_percent", hue="type")
plt.title('The overal distribution of User Profile using RFM Model')

# Show the plot
plt.show()
```

<img width="1694" height="701" alt="image" src="https://github.com/user-attachments/assets/d1cec52b-e305-4574-9f5a-88a5096e17bf" />

Defination:

- Segment: RFM
- User contribution: % user (có spending) theo segment
- Spending contribution: % spending (có spending) theo segment

### 5.2. Royal & Non royal

#### a. Visualize Customer Allocation by Loyal Status and Average Purchase Amount Thresholds

```python
# Calculate loyal_customer_volume and non_loyal_customer_volume
loyal_customer_volume = RFM_df_final[RFM_df_final['loyal_status'] == 'Loyal']['CustomerID'].nunique()
non_loyal_customer_volume = RFM_df_final[RFM_df_final['loyal_status'] == 'Non Loyal']['CustomerID'].nunique()

# Group by Quantity_average_bin and count CustomerID
df = RFM_df_final[['CustomerID', 'Quantity_average_bin', 'loyal_status']].groupby(['Quantity_average_bin', 'loyal_status']).count().reset_index().rename(columns={'CustomerID': 'Customer_volume'})

# Calculate Customer_percent
df['Customer_percent'] = df.apply(
    lambda x: (x.Customer_volume / loyal_customer_volume) * 100 if x.loyal_status == 'Loyal' else (x.Customer_volume / non_loyal_customer_volume) * 100,
    axis=1
)

# Drop Customer_volume column
df = df.drop(columns=['Customer_volume'])

# Pivot table to prepare for plotting
df_pivot = df.pivot(index='loyal_status', values='Customer_percent', columns='Quantity_average_bin')

# Plot the 100% stacked bar chart
df_pivot.plot(kind='bar', stacked=True, figsize=(10, 6), title = 'Stacked Bar chart showing Customer Distribution by Loyal Status and Average Purchase Amount Thresholds')
```

<img width="920" height="602" alt="image" src="https://github.com/user-attachments/assets/de2157ac-605e-4bf1-81e9-a36cbc098680" />

Defination:

- Quantity_average_bin: average purchase threshold
- Example: q1 < 6 -> Average customer group buys less than 6 products per order

#### b. Visualize Customer Allocation by Loyal Status and Average Purchase Price Thresholds

```python
# Ensure loyal_customer_volume and non_loyal_customer_volume are calculated
loyal_customer_volume = RFM_df_final[RFM_df_final['loyal_status'] == 'Loyal']['CustomerID'].nunique()
non_loyal_customer_volume = RFM_df_final[RFM_df_final['loyal_status'] == 'Non Loyal']['CustomerID'].nunique()

# Group by Quantity_average_bin and count CustomerID
df = RFM_df_final[['CustomerID', 'Cost_average_bin', 'loyal_status']].groupby(['Cost_average_bin', 'loyal_status']).count().reset_index().rename(columns={'CustomerID': 'Customer_volume'})

# Calculate Customer_percent
df['Customer_percent'] = df.apply(
    lambda x: (x.Customer_volume / loyal_customer_volume) * 100 if x.loyal_status == 'Loyal' else (x.Customer_volume / non_loyal_customer_volume) * 100,
    axis=1
)

# Drop Customer_volume column
df = df.drop(columns=['Customer_volume'])

# Pivot table to prepare for plotting
df_pivot = df.pivot(index='loyal_status', values='Customer_percent', columns='Cost_average_bin')

# Plot the 100% stacked bar chart
df_pivot.plot(kind='bar', stacked=True, figsize=(10, 6), title = 'Stacked Bar chart showing Customer Distribution by Loyal Status and Average Purchase Price Thresholds')
```

<img width="895" height="602" alt="image" src="https://github.com/user-attachments/assets/1b223d4f-bf43-4817-b5e9-47a1774e6079" />

Definition:
- Cost_average_bin: average value of each order
- Example: q1 < 12 -> Group of customers who pay less than $12 per order

#### c. Visualize Customer Allocation by Loyal Status and First Quantity

```python
# Group by First Quantity bin and count CustomerID
df_first_qty = RFM_df_final[['CustomerID', 'First Quantity bin', 'loyal_status']] \
    .groupby(['First Quantity bin', 'loyal_status']).count().reset_index().rename(columns={'CustomerID': 'Customer_volume'})

# Calculate Customer_percent
df_first_qty['Customer_percent'] = df_first_qty.apply(
    lambda x: (x.Customer_volume / loyal_customer_volume) * 100 if x.loyal_status == 'Loyal' 
              else (x.Customer_volume / non_loyal_customer_volume) * 100,
    axis=1
)

# Drop Customer_volume column
df_first_qty = df_first_qty.drop(columns=['Customer_volume'])

# Pivot table
df_pivot_first_qty = df_first_qty.pivot(index='loyal_status', values='Customer_percent', columns='First Quantity bin')

# Plot
df_pivot_first_qty.plot(kind='bar', stacked=True, figsize=(10,6),
                        title='Stacked Bar chart Customer Distribution by Loyal Status and First Quantity')
```

<img width="831" height="602" alt="image" src="https://github.com/user-attachments/assets/9fb3a600-1058-4eee-8c0a-8e156911aa9b" />

#### d. Visualize Customer Allocation by Loyal Status and First Cost

```python
# Group by First Cost bin and count CustomerID
df_first_cost = RFM_df_final[['CustomerID', 'First cost bin', 'loyal_status']] \
    .groupby(['First cost bin', 'loyal_status']).count().reset_index().rename(columns={'CustomerID': 'Customer_volume'})

# Calculate Customer_percent
df_first_cost['Customer_percent'] = df_first_cost.apply(
    lambda x: (x.Customer_volume / loyal_customer_volume) * 100 if x.loyal_status == 'Loyal' 
              else (x.Customer_volume / non_loyal_customer_volume) * 100,
    axis=1
)

# Drop Customer_volume column
df_first_cost = df_first_cost.drop(columns=['Customer_volume'])

# Pivot table
df_pivot_first_cost = df_first_cost.pivot(index='loyal_status', values='Customer_percent', columns='First cost bin')

# Plot
df_pivot_first_cost.plot(kind='bar', stacked=True, figsize=(10,6),
                         title='Stacked Bar chart Customer Distribution by Loyal Status and First Cost')
```

<img width="831" height="602" alt="image" src="https://github.com/user-attachments/assets/2027ae6e-07e5-4c61-b991-8b68c39cc9ab" />

## 6. 🔎 Insights & Recommendations
### 6.1. RFM Model

1. At Risk Customer and Cannot Lose Them Customer are two important customer groups (most of the customers and contribute the most revenue). However, the large proportion of At Risk and Cannot Lose Them groups is a warning sign. Due to the characteristics of these customers, they have not used the product for a long time, and are likely to abandon the product

    -> Actions: Promotional campaigns, or appropriate notifications to encourage customers to use the product.

2. Loyal, New Customer, Potential Loyalist, and Promising groups account for the majority of customers. However, most of these are customers with low transaction value (contributing modest revenue)

    -> Actions: Promote cross-selling campaigns, encourage consumption,...

### 6.1. Royal & Non Royal

1. Average purchase quantity
- Loyal Customer is a Customer whose number of transactions in 1 order is not too large (< 15 products in 1 order) -> This can be an individual customer but loyal and create long-term value

    -> Actions: Attract this group of potential customers through advertising strategies, Marketing, ...

2. Average purchase price
- Loyal Customer is a Customer whose transaction value in 1 order is not too large (< 18 dollars for 1 order -> This can be an individual customer, focusing on lower-priced product segments but loyal and create long-term value

    -> Actions: Attract this group of potential customers through advertising strategies, Marketing, ...

3. First purchase quantity
- Loyal customers do not necessarily start with a large order, but have stability from the first purchase.

- Non-Loyal has many large buyers from the beginning but does not maintain loyalty → they are likely to only buy 1-2 times and then leave.

    -> Action: For new customers who buy a lot (bin q4), need to implement a retention program early to turn them into loyal customers. Customers who buy little the first time (bin q1) but sustainably → focus on nurturing and upselling.

4. First purchase price
- High first order value does not mean loyalty.

- Loyal customers tend to spend moderately at first but maintain regularly.

- Non-Loyal sometimes spend a lot right away but not sustainably, easily "one time and that's it".

    -> Action: For customers who spend a lot of money the first time (q4) but are not Loyal → need a care/gratitude program to retain them. Use this insight to classify new customers: "spend a lot of money the first time + not Loyal" → target retention marketing campaigns immediately.


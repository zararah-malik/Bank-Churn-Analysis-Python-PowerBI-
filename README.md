# Bank Customer Churn Analysis

## 1. Introduction

A leading bank observed a significant number of customers closing their accounts — a phenomenon known as **churn**. To help the business understand the root causes, I conducted a data-driven analysis on a dataset of **10,000 customers**.

This case study aims to uncover the key factors behind customer churn and provide **actionable insights** that can support the bank’s customer retention strategies.  

Through step-by-step data cleaning, exploration, and visualization, this project turns raw data into a clear story that helps answer:  
- Who is leaving the bank?
- Why are they leaving?
- What can be done to reduce churn?

Let's dive in.
---

## 3. Skills & Tools Used

This case study involved both programming and data visualization to extract meaningful insights. Here’s what I used:

- **Python (Pandas, Seaborn, Matplotlib)**: For data cleaning, transformation, and exploratory analysis.
- **Power BI**: To design an interactive and visual dashboard that tells a complete story.
- **DAX (Data Analysis Expressions)**: To calculate key metrics such as churn rate, active vs exited customers, etc.
- **Data Cleaning & Preparation**: Segmented age groups, handled nulls, and converted columns to readable categories.
- **Analytical Thinking**: Identified trends, patterns, and behaviors behind customer churn.
---

## 4. How I Approached It

To uncover the reasons behind customer churn, I followed a structured step-by-step process:
# Used Python to Preprocess Data:
### 🔹 Step 1: Imported the Data
I began by importing the dataset and setting it up for analysis.
```python
import pandas as pd
df = pd.read_csv("Bank_Churn.csv")
df.head(10)
```

### 🔹 Step 2: Checked the Structure
I reviewed the shape, data types, summary statistics, and checked for any duplicate records.
```python
print("Shape of dataset:", df.shape)
```
```python
print("Missing Values:", df.isnull().sum())
```
```python
print("Data Types:", df.dtypes)
```
```python
duplicates = df.duplicated().sum()
print("Number of duplicate rows:", duplicates)
```
##### Checked For Summary Statistics:
```python
print("Summary Stats:", df.describe(include='all'))
```
### 🔹 Step 3: Cleaned the Data
I:
- Renamed columns for better readability
- Trimmed extra spaces
- Converted data types to make the dataset consistent and easier to work with
### 🔹 Step 4: Handled Outliers
I identified some extreme values. Rather than removing them, I chose to keep them because they might reveal important customer behaviors that lead to churn.
```python
# There is a Nan or $- lurking in a table column balance with some extra spaaces.
# Replacing that value with a 0.0 float number and make data consistent.
df['Balance'] = df['Balance'].str.replace(r'[\$,]', '', regex=True).str.strip()

# Step 2: Replace '-' or empty strings with 0
df['Balance'] = df['Balance'].replace({'-': '0', '': '0'})
# Know Changing the Type of Balance column
df['Balance'] = df['Balance'].astype(float)
```
##### Trimmed the Column names for better Access:
```python
df.columns = df.columns.str.strip()
```
```python
df['EstimatedSalary'] = df['EstimatedSalary'].str.replace(r'[\$,]', '', regex=True).str.strip()
df['EstimatedSalary'] = df['EstimatedSalary'].astype(float)
```
### 🔹 Step 5: Correlation Check
I created a heatmap to understand how different numerical features are related to each other — especially to the churn column.
```python
numeric_df = df.select_dtypes(include=['int64', 'float64'])

# Compute correlation matrix
corr_matrix = numeric_df.corr()

# Plot heatmap
plt.figure(figsize=(10, 8))
sns.heatmap(corr_matrix, annot=True, cmap='coolwarm', fmt=".2f", linewidths=0.5)
plt.title('Correlation Heatmap')
plt.tight_layout()
plt.show()
```
### 🔹 Step 6: Categorized Key Columns
To get clearer insights:
- I grouped customers into age categories like Young, Adult, Senior, and Retired
- I also categorized tenure and number of products used to spot behavioral patterns more easily
```python
def segment_age(age):
    if age <= 25:
        return 'Young (<=25)'
    elif 26 <= age <= 35:
        return 'Adult (26-35)'
    elif 36 <= age <= 45:
        return 'Mature (36-45)'
    elif 46 <= age <= 60:
        return 'Senior (46-60)'
    else:
        return 'Elderly (60+)'

# Apply the function to create a new column
df['Age Segment'] = df['Age'].apply(segment_age)
print("Data Types:",df['Age Segment'].dtypes)
print(df[['Age', 'Age Segment']].head(10))
```
### 🔹 Step 7: Visualized in Power BI
Once the data was ready, I moved to Power BI to build an interactive dashboard.  
I added slicers for Age, Gender, and Geography, along with visuals like churn by tenure, product usage, and more — giving users the power to explore the data on their own.
Below is the Power BI dashboard I created to visualize churn behavior across different customer segments:

![Bank Customer Churn Dashboard](https://github.com/zararah-malik/Bank-Churn-Analysis-Python-PowerBI-/blob/main/Bank%20Churn%20Analysis%20Dashboard.png)
---

## 6. Key Insights & Recommendations  

### 🔍 Insight 1: Low Product Engagement  
**Problem**: A large portion of churned customers had only one product.  
**Action**: Filtered data by the number of products to identify trends.  
**Result**: Found that **63%** of customers who left had only **1 bank product**.  

**Recommendation**: Encourage multi-product usage by offering bundled services and loyalty rewards.

---

### 🔍 Insight 2: Inactive Accounts  
**Problem**: Many customers were no longer actively using their accounts.  
**Action**: Analyzed activity columns such as "IsActiveMember".  
**Result**: Nearly **80%** of churned customers were inactive in the last 3 months.

**Recommendation**: Engage inactive users through personalized messages or exclusive offers.

---

### 🔍 Insight 3: Age and Gender Risk Segments  
**Problem**: Churn behavior varied by age and gender.  
**Action**: Segmented data into age groups and analyzed churn trends.  
**Result**: **Seniors (46–60 years)** and **male customers** were more likely to leave.

**Recommendation**: Target these groups with specialized retention strategies like senior-specific services and trust-building incentives.

---

## 7. What I Can Do Further  

To further enrich the analysis, I can explore churn behavior based on **Average Balance** and **Estimated Salary** to uncover any hidden financial triggers behind customer exits.  

These additional visuals could provide deeper context into financial habits and help businesses take more targeted actions to retain high-value customers.

---
## 8. Conclusion  

This project helped uncover the hidden reasons behind customer churn in the banking sector.  
By analyzing customer behaviors across age, gender, product usage, and engagement levels,  
I was able to highlight patterns that can help drive smarter retention strategies.

The combination of data cleaning in Python and interactive storytelling with Power BI made the analysis both thorough and actionable.

Reducing churn isn't just about identifying who is leaving — it's about understanding **why** they leave, and taking steps to keep them longer.

This project reinforced my belief that with the right data approach, we can translate numbers into strategies that truly impact business outcomes.

---


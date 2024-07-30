# Customer vs Product sales analysis

This project analyzes sales data from the Diwali season. The analysis includes importing data, cleaning it, performing exploratory data analysis (EDA), and drawing conclusions about purchasing behaviors.

## Table of Contents
- [Introduction](#introduction)
- [Setup and Installation](#setup-and-installation)
- [Data Import and Cleaning](#data-import-and-cleaning)
- [Exploratory Data Analysis](#exploratory-data-analysis)
  - [Gender Analysis](#gender-analysis)
  - [Age Analysis](#age-analysis)
  - [State Analysis](#state-analysis)
  - [Marital Status Analysis](#marital-status-analysis)
  - [Occupation Analysis](#occupation-analysis)
  - [Product Category Analysis](#product-category-analysis)
- [Conclusion](#conclusion)


## Introduction
This project aims to provide insights into the sales data during Diwali. It includes steps to import, clean, and analyze data using Python libraries such as Pandas, NumPy, Matplotlib, and Seaborn.

## Setup and Installation
To run this project, you need to have Python installed. You can install the required libraries using pip:


    pip install numpy pandas matplotlib seaborn
    Data Import and Cleaning
    We start by importing necessary libraries and the dataset.

    import numpy as np
    import pandas as pd
    import matplotlib.pyplot as plt
    import seaborn as sns    
                                         `

## Load the dataset
    df = pd.read_csv('customer vs product sales analysis.csv', encoding='unicode_escape')

## Display the first few rows
    print(df.head())

![Screenshot 2024-07-30 134406](https://github.com/user-attachments/assets/ed57c82d-f853-49f7-890d-3e67a18ef753)


We then perform data cleaning by removing unnecessary columns and handling missing values.

    # Drop unrelated/blank columns
    df.drop(['Status', 'unnamed1'], axis=1, inplace=True)

    # Drop null values
    df.dropna(inplace=True)

    # Change data type of 'Amount'
    df['Amount'] = df['Amount'].astype('int')

# Exploratory Data Analysis
## Gender Analysis

### Plotting a bar chart for Gender and its count
    ax = sns.countplot(x='Gender', data=df)
    for bars in ax.containers:
    ax.bar_label(bars)
    plt.show()

![image](https://github.com/user-attachments/assets/250623da-5533-4966-bc55-7400fe613e73)

### Plotting a bar chart for gender vs total amount
    sales_gen = df.groupby(['Gender'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False)
    sns.barplot(x='Gender', y='Amount', data=sales_gen)
    plt.show()

![Screenshot 2024-07-30 194136](https://github.com/user-attachments/assets/637c27e9-0ade-4f1b-b26b-9a0344f924f4)    

## Age Analysis

### Plotting a bar chart for Age Group and its count
    ax = sns.countplot(data=df, x='Age Group', hue='Gender')
    for bars in ax.containers:
    ax.bar_label(bars)
    plt.show()

![Screenshot 2024-07-30 194420](https://github.com/user-attachments/assets/a437f13e-7a32-40f2-a759-f8e26ee6d51f)

### Total Amount vs Age Group
    sales_age = df.groupby(['Age Group'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False)
    sns.barplot(x='Age Group', y='Amount', data=sales_age)
    plt.show()


![image](https://github.com/user-attachments/assets/ef753fd5-2168-4a12-856d-dbedd02c75d9)

## State Analysis

### Total number of orders from top 10 states
    sales_state = df.groupby(['State'], as_index=False)['Orders'].sum().sort_values(by='Orders', ascending=False).head(10)
    sns.barplot(data=sales_state, x='State', y='Orders')
    plt.show()

![image](https://github.com/user-attachments/assets/5854eb1e-1128-462a-a11f-5b432ef59711)

### Total amount/sales from top 10 states
    sales_state = df.groupby(['State'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False).head(10)
    sns.barplot(data=sales_state, x='State', y='Amount')
    plt.show()

![image](https://github.com/user-attachments/assets/1c6e135d-6867-44cc-8970-ff523bb6737d)

From above graphs we can see that most of the orders & total sales/amount are from Uttar Pradesh, Maharashtra and Karnataka respectively

## Marital Status Analysis

### Plotting a bar chart for Marital Status
    ax = sns.countplot(data=df, x='Marital_Status')
    for bars in ax.containers:
    ax.bar_label(bars)
    plt.show()

![image](https://github.com/user-attachments/assets/873fe803-7149-46ed-9fff-923b2967cb6f)

### Amount by Marital Status and Gender
    sales_state = df.groupby(['Marital_Status', 'Gender'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False)
    sns.barplot(data=sales_state, x='Marital_Status', y='Amount', hue='Gender')
    plt.show()

![image](https://github.com/user-attachments/assets/18ae7684-f6fe-4dbe-8f2c-961e34f05ff4)

From above graphs we can see that most of the buyers are married (women) and they have high purchasing power

## Occupation Analysis

### Plotting a bar chart for Occupation
    sns.countplot(data=df, x='Occupation')
    plt.show()

![image](https://github.com/user-attachments/assets/c782ec17-fba7-4b59-9bcb-701170d7705b)

### Amount by Occupation
    sales_state = df.groupby(['Occupation'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False)
    sns.barplot(data=sales_state, x='Occupation', y='Amount')
    plt.show()

![image](https://github.com/user-attachments/assets/240f59bd-34b2-4009-b21d-3bd430922d3b)

From above graphs we can see that most of the buyers are working in IT, Healthcare and Aviation sector

## Product Category Analysis

### Plotting a bar chart for Product Category
    sns.countplot(data=df, x='Product_Category')
    plt.show()

![image](https://github.com/user-attachments/assets/bbdb3c63-b836-47e6-bcbe-55292053c900)

### Amount by Product Category
    sales_state = df.groupby(['Product_Category'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False).head(10)
    sns.barplot(data=sales_state, x='Product_Category', y='Amount')
    plt.show()

![image](https://github.com/user-attachments/assets/12f7ad07-d3f3-4405-bf7c-cb52eb0f652a)

From above graphs we can see that most of the sold products are from Food, Clothing and Electronics category

## Conclusion
Married women aged 26-35 years from Uttar Pradesh, Maharashtra, and Karnataka, working in IT, Healthcare, and Aviation are more likely to buy products from Food, Clothing, and Electronics categories.

# UPI Transactions Dashboard

### Dashboard Link : https://app.powerbi.com/links/IVHCWt-7aW?ctid=e9f53682-9dc4-428b-ba7b-b55c3de07e9b&pbi_source=linkShare

## Problem Statement

This dashboard aims to provide a comprehensive overview and analysis of UPI (Unified Payments Interface) transaction data. The primary goal is to help stakeholders understand key trends, identify patterns, and gain actionable insights into transaction volumes, values, and user behavior over time and across different dimensions. This understanding can be crucial for strategic decision-making, operational efficiency, and identifying areas for growth or concern within the UPI ecosystem.

## Dataset

The primary dataset used for this report is `UPI+Transactions.xlsx - Sheet1.csv`, which was likely combined with data imported from a SQL database. It contains detailed information about UPI transactions, forming the foundation for all analyses and visualizations in the dashboard.

## Steps Followed

-   **Step 1: Data Acquisition - Loading from SQL Server and CSV.**
    * **From SQL Server:** Connected to a SQL Server database to import relevant tables or views containing UPI transaction data. This involved using the "Get Data" -> "SQL Server database" option in Power BI Desktop and writing appropriate SQL queries to fetch the required information.
    * **From CSV File:** The `UPI+Transactions.xlsx - Sheet1.csv` file was also loaded into Power BI Desktop, likely to supplement or merge with the SQL data.
-   **Step 2: Data Profiling in Power Query Editor.**
    * Opened Power Query Editor to inspect the loaded data.
    * In the "View" tab under the "Data Preview" section, "Column Distribution" , "Column Quality", and "Column Profile" options were checked to understand the data's integrity and characteristics.
    * "Column profiling based on entire dataset" was selected for a comprehensive analysis, extending beyond the default 1000 rows.
    * It was observed that in none of the columns errors & empty values were present except column named "Arrival Delay". (Note: This might be a leftover from the Airlines dataset description, please verify for UPI data).
-   **Step 3: Data Transformation (Power Query).**
    * Common transformations for transaction data were performed, such as changing data types for dates, numbers, and text columns to ensure correct calculations and filtering.
    * Ensured proper formatting and cleansing of transaction-related fields for consistency.
    * If multiple tables were involved (from SQL and/or CSV), appropriate merging or appending operations were performed to create a consolidated view relevant for analysis.
    * For calculating average delay time, null values in the "Arrival Delay" column were not taken into account as only less than 1% values were null. (Note: This also seems to be from the Airlines dataset; please adapt or remove if not relevant to UPI data).
-   **Step 4: Data Modeling.**
    * Relationships were established between different tables (e.g., between transaction data from SQL and supplementary data from CSV, or any dimension tables imported from SQL) ensuring an optimized schema for performance and accurate calculations.
-   **Step 5: DAX Calculations.**
    * **Total Transaction Value:** A measure was created to calculate the sum of all transaction amounts.
        ```dax
        Total Transaction Value = SUM('YourTableName'[Amount]) // Adjust 'YourTableName' and 'Amount' to your actual column names
        ```
    * **Total Number of Transactions:** A measure to count the total number of UPI transactions.
        ```dax
        Total Transactions = COUNTROWS('YourTableName') // Adjust 'YourTableName' to your actual table name
        ```
    * **Age Group Calculated Column:** A calculated column was created to group customers into various age groups.
        ```dax
        Age Group =
        if(YourTable[Age]<=25, "0-25 (25 included)",
        if(YourTable[Age]<=50, "25-50 (50 included)",
        if(YourTable[Age]<=75, "50-75 (75 included)",
        "75-100 (100 included)"))) // Adjust 'YourTable' and 'Age'
        ```
        ![Snap_1](https://user-images.githubusercontent.com/102996550/174089602-ab834a6b-62ce-4b62-8922-a1d241ec240e.jpg)
    * **Count of Customers Measure:** A measure to find the total count of customers.
        ```dax
        Count of Customers = COUNT(YourTable[ID]) // Adjust 'YourTable' and 'ID'
        ```
        ![Snap_Count](https://user-images.githubusercontent.com/102996550/174090154-424dc1a4-3ff7-41f8-9617-17a2fb205825.jpg)
    * **% Customers Measure:** A measure to calculate the percentage of customers (e.g., preferred business class, as per original text).
        ```dax
        % Customers = (DIVIDE(YourTable[Count of Customers], TotalOverallCustomers)*100) // Adjust 'YourTable' and 'TotalOverallCustomers'
        ```
       ![Snap_Percentage](https://user-images.githubusercontent.com/102996550/174090653-da02feb4-4775-4a95-affb-a211ca985d07.jpg)
    * **Total Distance Travelled Measure:** A measure to calculate the total distance travelled (from original text, adjust if not applicable to UPI).
        ```dax
        Total Distance Travelled = SUM(YourTable[Flight Distance]) // Adjust 'YourTable' and 'Flight Distance'
        ```
        ![Snap_3](https://user-images.githubusercontent.com/102996550/174091618-bf770d6c-34c6-44d4-9f5e-49583a6d5f68.jpg)
-   **Step 6: Dashboard Design & Visualization.**
    * A suitable theme was selected for the report.
    * **Slicers:** Visual filters (Slicers) were added for fields like "Class", "Customer Type", "Gate Location" & "Type of travel". (Note: These are from the Airlines data, please update to relevant UPI dimensions like "State", "Transaction Type", "Bank", "Year/Month").
    * **Card Visuals:** Card visuals were used to display key performance indicators (KPIs) like "average departure delay in minutes" and "average arrival delay in minutes". (Again, from Airlines data, please update to UPI KPIs like "Total Transaction Value", "Number of Transactions", "Average Transaction Value"). Visual level filters were used for average calculations, although blank values are typically ignored by default.
    * **Bar Chart:** A bar chart was added representing the number of satisfied & neutral/unsatisfied customers."Gender" was added to the Legends bucket for segmentation.

-   **Step 7: Publishing to Power BI Service.** The report was then published to the Power BI Service
## Dashboard Snapshots

Here are snapshots of the UPI Transactions Dashboard, showcasing its design and key visuals:

**Page 1:**
![Image](https://github.com/user-attachments/assets/2f3589d4-a9c6-4192-b996-0d1b1dedc84e)

**Page 2:**
![Image](https://github.com/user-attachments/assets/e28687a3-d54e-40c3-8310-56f95c728ba6)

## Key Insights

A two-page report was created on Power BI Desktop and it was then published to Power BI Service. The following types of inferences can be drawn from the dashboard:

* **Total Number of Customers/Transactions:** A clear count of the overall engagement (e.g., Total Number of Customers = 129880).
    * (Original text provided a breakdown of satisfied/unsatisfied customers by gender. You'll need to replace this with UPI-specific insights, e.g., breakdown of transactions by successful/failed, or by customer type).
* **Average Metrics:** Insights into average transaction value or volume per period/category.
    * (Original text listed average ratings for various services. You will replace these with average UPI-related metrics.)
    * Average metrics will change if different visual filters are applied.
* **Categorical Analysis:**
    * **By Class/Transaction Type:** Understanding distribution across different types of transactions or user segments (e.g., 47.87 % customers travelled by Business class. This needs to be replaced with UPI-specific categories like "Peer-to-Peer," "Merchant Payments," etc.).
    * **By Age Group:** Insights into the demographics of users (e.g., maximum customers belong to '25-50' age group).
    * **By Customer Type:** Distinction between new and returning users (e.g., more customers have customer type 'returning').
    * **By Type of Travel/Purpose:** Analysis based on the purpose of transactions (e.g., more customers have travel type 'Business'. This needs to be replaced with UPI transaction purposes).

## Technologies Used

* **Microsoft Power BI Desktop:** For data loading, transformation, modeling, and visualization.
* **SQL Server:** For querying and importing data from relational databases.
* **Power Query (M Language):** For robust data extraction, cleaning, and transformation.
* **DAX (Data Analysis Expressions):** For creating calculated columns and measures to derive deeper insights.
* **Microsoft Excel/CSV:** As an additional data source.

---

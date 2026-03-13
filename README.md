# Olist E-commerce Analytics Dashboard (Power BI)

This project presents an interactive **Power BI dashboard** built using the **Olist Brazilian e-commerce dataset**.  
The goal of the project was to transform raw transactional data into a structured analytical model and create a dashboard that enables analysis of sales performance, customer behavior, delivery efficiency, and regional distribution of orders.

The report combines:

- data transformation in Power Query  
- a structured data model  
- DAX measures  
- interactive visualizations  

---

# Dashboard

![Dashboard](images/dashboard.png)

The dashboard provides a high-level overview of business performance using KPI indicators such as:

- **Total Revenue**
- **Total Orders**
- **Late Orders Rate**
- **Total Customers**

Additional visuals allow exploration of:

- weekly order trends  
- monthly performance metrics  
- revenue by payment type  
- top product categories  

---

# Geographic Analysis

![Map](images/map.png)

The report includes a geographic visualization showing the distribution of orders across Brazilian states.

The map uses:

- **bubble size** to represent order volume  
- **tooltips** to display additional information such as revenue, number of customers, and delivery performance.

This allows quick identification of regions with the highest concentration of orders.

---

# Data Model

![Data Model](images/data_model.png)

The report is built on a relational model integrating several tables from the Olist dataset.

The structure follows a **star-like schema**, where the **Orders** table acts as the central fact table connected to dimension tables.

### Dimension tables
- Customer  
- Seller  
- Product  
- Date  

### Fact tables
- Orders  
- Order Items  
- Order Payments  
- Order Reviews  

To keep the model organized and maintainable, all calculations were placed in a dedicated **Measures** table.

---

# Measures

![Measures](images/measures.png)

![Measures](images/measures_2.png)

All DAX calculations were organized in a dedicated table called **Measures**.  
This improves readability and helps separate business logic from raw data tables.

Examples of implemented measures include:

- Total Revenue  
- Total Orders  
- Total Customers  
- Average Order Value  
- Average Review Score  
- Average Shipping Days  
- Late Orders  
- Late Orders Rate  
- Canceled Orders  
- Product Orders  
- Product Value  
- previous month comparison measures  

These measures power KPI cards, trend charts, and analytical visuals across the report.

---

# Custom Tooltips

To provide additional contextual insights without overcrowding the main visuals, the report includes **custom tooltip pages**.

### Chart Tooltip

![Chart Tooltip](images/chart_tooltips.png)

This tooltip is used in the weekly orders trend chart and displays detailed information about the selected date, including the number of orders.

---

### Map Tooltip

![Map Tooltip](images/map_tooltips.png)

The map tooltip displays additional regional information such as:

- state  
- total orders  
- total revenue  
- total customers  
- average shipping days  
- canceled orders rate  

This improves the analytical value of the geographic visualization.

---

# Data Preparation (Power Query)

Data cleaning and transformation were performed in **Power Query**.

Key steps included:

- assigning correct data types (text, currency, date, datetime)  
- removing rows with errors or missing values  
- renaming columns into more readable business labels  
- creating surrogate keys using index columns  
- merging selected tables with the Orders table to retrieve internal model keys  
- standardizing text values (for example replacing underscores and applying proper case)  
- removing columns not required for reporting  

The **Category Translation** table was used to enrich product categories with English names and was disabled from load after the final category field was created.

The **Geolocation** table was also excluded from the final model because the report focuses on state-level geographic analysis.

---

# Date Modeling

A dedicated **Date dimension** was created using **DAX** to support time-based analysis.

The table includes fields such as:

- Date  
- Year  
- Month  
- Day  
- Month Name  
- Week Day  
- Weekend indicator  
- Quarter  
- Week Number  
- Week Start Date  

Additionally, several datetime columns in the **Orders** table were converted into separate date fields to simplify analysis:

- Purchase Date  
- Approved Date  
- Carrier Delivery Date  
- Customer Delivery Date  
- Delivery Estimated Date  

Additional calculated columns were also created to support delivery analysis:

- Delivery Days  
- Is Late  
- Late Days  

Using separate date fields improves filtering, grouping, and time-based calculations.

---

# Model Optimization

To make the semantic model cleaner and easier to use, several technical fields were hidden from report view.

These include:

- internal ID columns  
- foreign keys used only for relationships  
- original datetime columns replaced by date fields  
- helper columns created during transformation  

This approach improves usability and keeps the model focused on business-friendly fields.
- custom tooltip implementation  
- business intelligence reporting  

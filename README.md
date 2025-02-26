# 📊 Sales Analysis & SQL Insights

## 🚀 Project Overview
This project focuses on **Sales Data Analysis** using Python, SQL, and Google Sheets. The goal is to clean and process raw sales data, generate insights, and visualize key metrics using dashboards. Additionally, a Google Apps Script automates highlighting pending orders older than 30 days.

## 📂 Dataset Details
- **Initial Dataset**: Contains raw e-commerce sales transactions, including date, customer info, product details, revenue, payment method, and delivery status.
- **Processed Dataset**: Cleaned version with duplicate removal, data validation, and added computed fields for deeper analysis.

## 🔧 Tech Stack & Tools
- **Python (Pandas, Seaborn, Matplotlib)** – Data Cleaning, Analysis & Visualization
- **SQL** – Querying & Extracting Insights
- **Google Sheets & Apps Script** – Dashboarding & Automation

---

## 📊 Key Analyses & Insights
### **1️⃣ Data Cleaning & Validation**
- Removed duplicates & handled missing values
- Converted numeric fields to correct data types
- Applied data validation for Product Category & Payment Method

### **2️⃣ Revenue Analysis**
- Computed **total revenue per product category**
- Identified **top 5 best-selling products**
- Analyzed which **payment method generates the highest revenue**

### **3️⃣ Customer Insights**
- Found the **top 3 highest-spending customers**
- Counted unique customers & multiple purchases on the same day

### **4️⃣ Delivery Performance**
- Calculated % of **pending, delivered, and canceled orders**
- Applied **conditional formatting** to highlight pending (yellow), delivered (green), and canceled (red) orders

### **5️⃣ Dashboard & Visualizations**
✅ **Total Revenue** Summary  
✅ **Top 3 Best-Selling Products**  
✅ **Pie Chart** for Payment Methods  
✅ **Bar Chart** for Sales per Product Category  

---

## 🛠️ SQL Queries Used
### **1️⃣ Total Revenue per Product Category**
```sql
SELECT product_category, SUM(total_revenue) AS total_revenue 
FROM sales_data 
GROUP BY product_category 
ORDER BY total_revenue DESC;
```
### **2️⃣ Top 5 Best-Selling Products by Revenue**
```sql
SELECT product_name, SUM(total_revenue) AS total_revenue 
FROM sales_data 
GROUP BY product_name 
ORDER BY total_revenue DESC 
LIMIT 5;
```
### **3️⃣ Count Orders by Payment Method**
```sql
SELECT payment_method, COUNT(order_id) AS total_orders 
FROM sales_data 
GROUP BY payment_method;
```
### **4️⃣ Identify Customers Making Multiple Purchases in a Day**
```sql
SELECT customer_name, order_date, COUNT(order_id) AS order_count 
FROM sales_data 
GROUP BY customer_name, order_date 
HAVING order_count > 1;
```
### **5️⃣ Most Frequent Customer by Orders**
```sql
SELECT customer_name, COUNT(order_id) AS total_orders 
FROM sales_data 
GROUP BY customer_name 
ORDER BY total_orders DESC 
LIMIT 1;
```

---

## 📝 Google Apps Script for Automation
This script **highlights pending orders older than 30 days** in Google Sheets.
```javascript
function highlightOldPendingOrders() {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName("Cleaned_Data");
  if (!sheet) {
    Logger.log("Error: Sheet not found.");
    return;
  }

  var data = sheet.getDataRange().getValues();
  var today = new Date();

  for (var i = 1; i < data.length; i++) {
    var orderDate = new Date(data[i][1]);
    var status = data[i][9];

    if (!isNaN(orderDate) && status === "Pending") {
      var diffDays = (today - orderDate) / (1000 * 3600 * 24);
      if (diffDays > 30) {
        sheet.getRange(i + 1, 1, 1, sheet.getLastColumn()).setBackground("red");
      }
    }
  }
}
```

---

## 📂 Files Included
📌 `Initial_Dataset.xlsx` – Raw sales data  
📌 `Processed_Dataset.xlsx` – Cleaned and analyzed data  
📌 `sales_analysis.ipynb` – Jupyter Notebook with full Python analysis  
📌 `google_script.js` – Google Apps Script for automation  
📌 `dashboard.png` – Visual representation of key metrics  

---

## 🚀 How to Run This Project
1. **For SQL Queries**: Use MySQL/PostgreSQL to execute queries on `sales_data` table.
2. **For Python Analysis**:
   - Open `sales_analysis.ipynb` in Jupyter Notebook/Google Colab
   - Install dependencies: `pip install pandas matplotlib seaborn`
   - Run all cells to generate insights
3. **For Google Apps Script**:
   - Open Google Sheets, go to **Extensions > Apps Script**
   - Paste `google_script.js` code and run it

---

## ⭐ Contributing
Feel free to **fork this repository**, create a new branch, and submit a **pull request** if you have improvements or new insights to add!

---

## 📬 Contact
📧 Email: vratesh9405@gmail.com  
🔗 LinkedIn: [Your LinkedIn Profile]  


# UPI-Payment-Transactions
The dataset in this project contains simulated data of UPI (Unified Payments Interface) transactions, which are a popular method of transferring funds between bank accounts in India. UPI allows users to send and receive money using virtual payment addresses (VPAs) linked to their bank accounts.

Here are some questions a data analyst might explore using the **UPI Transactions Dataset**, along with explanations and suggestions for creating visualizations in Power BI:

---

### **1. What is the distribution of transaction statuses (SUCCESS vs. FAILED)?**
- **Visualization**: Create a **Pie Chart** or **Clustered Bar Chart**.
- **Steps**:
  1. Drag the `Status` field to the **Axis** (or Legend for Pie Chart).
  2. Drag `Transaction ID` or a count of transactions to the **Values** field.
  3. Customize the colors to differentiate between SUCCESS and FAILED.
- **Insights**: Understand the proportion of successful vs. failed transactions.

---

### **2. What is the total transaction amount grouped by status?**
- **Visualization**: Use a **Stacked Bar Chart** or **Clustered Column Chart**.
- **Steps**:
  1. Drag `Status` to the **Axis** field.
  2. Drag `Amount (INR)` to the **Values** field and set it to **Sum**.
  3. Add data labels to display total amounts.
- **Insights**: Compare how much money was successfully transferred vs. failed transactions.

---

### **3. What is the average transaction amount across different sender banks?**
- **Visualization**: Use a **Bar Chart** or **Line Chart**.
- **Steps**:
  1. Extract the bank identifiers from `Sender UPI ID` using **Power Query** or a calculated column.
     ```DAX
     SenderBank = RIGHT('Transactions'[Sender UPI ID], LEN('Transactions'[Sender UPI ID]) - FIND("@", 'Transactions'[Sender UPI ID]))
     ```
  2. Drag the calculated column `SenderBank` to the **Axis** field.
  3. Drag `Amount (INR)` to the **Values** field and set it to **Average**.
- **Insights**: Identify which banks handle larger or smaller transactions on average.

---

### **4. How do transaction amounts vary over time?**
- **Visualization**: Use a **Line Chart** or **Area Chart**.
- **Steps**:
  1. Drag `Timestamp` to the **Axis** field and set it to display by **Day/Month/Year**.
  2. Drag `Amount (INR)` to the **Values** field and set it to **Sum**.
- **Insights**: Analyze trends such as spikes in transactions during specific periods (e.g., festivals or paydays).

---

### **5. What is the average transaction amount by transaction status?**
- **Visualization**: Use a **Clustered Bar Chart**.
- **Steps**:
  1. Drag `Status` to the **Axis** field.
  2. Drag `Amount (INR)` to the **Values** field and set it to **Average**.
- **Insights**: Understand if failed transactions tend to have higher or lower amounts compared to successful ones.

---

### **6. Which sender-receiver pairs have the highest transaction amounts?**
- **Visualization**: Use a **Table** or **Matrix**.
- **Steps**:
  1. Drag `Sender Name` and `Receiver Name` to the **Rows** field.
  2. Drag `Amount (INR)` to the **Values** field and set it to **Sum**.
  3. Sort the table/matrix by transaction amount in descending order.
- **Insights**: Highlight key relationships for high-value transactions.

---

### **7. Which banks have the highest transaction failure rates?**
- **Visualization**: Use a **Bar Chart** with calculated fields.
- **Steps**:
  1. Create a calculated column to extract the bank from `Sender UPI ID`:
     ```DAX
     SenderBank = RIGHT('Transactions'[Sender UPI ID], LEN('Transactions'[Sender UPI ID]) - FIND("@", 'Transactions'[Sender UPI ID]))
     ```
  2. Create a measure for failure rates:
     ``` DAX
     FailureRate = DIVIDE(
         COUNTROWS(FILTER('Transactions', 'Transactions'[Status] = "FAILED")),
         COUNTROWS('Transactions')
     )
     ```
  3. Use a Bar Chart, with `SenderBank` on the **Axis** and `FailureRate` on the **Values**.
- **Insights**: Identify banks with operational issues.

---

### **8. What are the top 10 transactions by amount?**
- **Visualization**: Use a **Table** with filters.
- **Steps**:
  1. Drag `Transaction ID`, `Sender Name`, `Receiver Name`, and `Amount (INR)` into the **Columns** field.
  2. Apply a filter on `Amount (INR)` to show the **Top 10** by value.
- **Insights**: Showcase significant transactions.

---

### **9. What are the peak transaction times during the day?**
- **Visualization**: Use a **Line Chart** or **Heat Map**.
- **Steps**:
  1. Extract the hour from `Timestamp` using Power Query or DAX:
     ```DAX
     TransactionHour = HOUR('Transactions'[Timestamp])
     ```
  2. Drag `TransactionHour` to the **Axis** field.
  3. Drag `Transaction ID` to the **Values** field and set it to **Count**.
- **Insights**: Identify when users are most active in transferring funds.

---

### **10. What is the percentage of failed transactions per bank?**
- **Visualization**: Use a **Stacked Bar Chart** or **100% Stacked Bar Chart**.
- **Steps**:
  1. Drag `SenderBank` to the **Axis ' field.
  2. Drag `Transaction ID` to the **Values** field and set it to **Count**.
  3. Drag `Status` to the **Legend** field.
  4. Format the chart to display percentages.
- **Insights**: Compare the failure rates of different banks visually.

---

### **Power BI Tips for Analysis**
- Use **Filters and Slicers**: Add slicers for `Timestamp`, `Status`, or `Amount (INR)` to allow users to focus on specific periods, statuses, or transaction ranges.
- Use **Drill-Through**: Enable drill-through to explore detailed transaction data for specific senders, receivers, or banks.
- Use **Bookmarks**: Create bookmarks for different analytical views, such as failure analysis, transaction trends, or bank-specific insights.

Let me know if you'd like detailed guidance on implementing any of these visualizations!


<img width="671" alt="Visual 1" src="https://github.com/user-attachments/assets/1788cd12-2f79-4780-b97d-14e6668dbcf4" />

<img width="664" alt="Visual 2" src="https://github.com/user-attachments/assets/47fc3f19-d1f5-435e-9485-c55db39bf953" />

<img width="669" alt="Visual 3" src="https://github.com/user-attachments/assets/07f47282-368a-4a3c-9485-e1c572ea7af7" />













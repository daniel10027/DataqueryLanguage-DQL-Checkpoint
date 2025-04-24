# 📊 DQL Queries – Customer/Product/Order Relational Model

This README provides a collection of **SQL queries** to retrieve data from a relational model consisting of three tables:

- `Customer(Customer_id, Customer_Name, Customer_Tel)`
- `Product(Product_id, Product_name, Category, Price)`
- `Orders(Customer_id, Product_id, OrderDate, Quantity, Total_amount)`

📌 Based on the relational model image: [View Model](https://i.imgur.com/Am5S7XF.png)

---

## ✅ SQL Queries (DQL)

### 1️⃣ Display all the data of customers

```sql
SELECT * FROM Customer;
```

---

### 2️⃣ Display the product_name and category for products which their price is between 5000 and 10000

```sql
SELECT product_name, category
FROM Product
WHERE Price BETWEEN 5000 AND 10000;
```

---

### 3️⃣ Display all the data of products sorted in descending order of price

```sql
SELECT * FROM Product
ORDER BY Price DESC;
```

---

### 4️⃣ Display the total number of orders, the average amount, the highest total amount and the lowest total amount

```sql
SELECT 
    COUNT(*) AS total_orders,
    AVG(total_amount) AS average_amount,
    MAX(total_amount) AS highest_amount,
    MIN(total_amount) AS lowest_amount
FROM Orders;
```

---

### 5️⃣ For each product_id, display the number of orders

```sql
SELECT Product_id, COUNT(*) AS number_of_orders
FROM Orders
GROUP BY Product_id;
```

---

### 6️⃣ Display the customer_id which has more than 2 orders

```sql
SELECT Customer_id
FROM Orders
GROUP BY Customer_id
HAVING COUNT(*) > 2;
```

---

### 7️⃣ For each month of the 2020 year, display the number of orders

```sql
SELECT 
    TO_CHAR(OrderDate, 'MM') AS month,
    COUNT(*) AS number_of_orders
FROM Orders
WHERE EXTRACT(YEAR FROM OrderDate) = 2020
GROUP BY TO_CHAR(OrderDate, 'MM')
ORDER BY month;
```

---

### 8️⃣ For each order, display the product_name, the customer_name and the date of the order

```sql
SELECT 
    O.OrderDate,
    C.Customer_Name,
    P.Product_name
FROM Orders O
JOIN Customer C ON O.Customer_id = C.Customer_id
JOIN Product P ON O.Product_id = P.Product_id;
```

---

### 9️⃣ Display all the orders made three months ago

```sql
SELECT *
FROM Orders
WHERE OrderDate BETWEEN ADD_MONTHS(SYSDATE, -3) AND LAST_DAY(ADD_MONTHS(SYSDATE, -3));
```

---

### 🔟 Display customers (customer_id) who have never ordered a product

```sql
SELECT Customer_id
FROM Customer
WHERE Customer_id NOT IN (
    SELECT DISTINCT Customer_id FROM Orders
);
```

---

# 🛒 E-Commerce Order Management System — MySQL Project

A hands-on intermediate-level SQL project built with MySQL, simulating a real-world e-commerce database with customers, orders, products, and payments.

---

## 📁 Project Structure

```
ecommerce-sql/
├── schema.sql        # Table definitions (DDL)
├── seed_data.sql     # Sample INSERT statements
├── queries.sql       # Practice queries (Level 1–5)
└── README.md
```

---

## 🗂️ Database Schema

### Tables

| Table          | Description                              |
|----------------|------------------------------------------|
| `categories`   | Product categories (Electronics, etc.)  |
| `products`     | Product catalog with price & stock       |
| `customers`    | Registered customer details              |
| `orders`       | Order headers with status tracking       |
| `order_items`  | Line items linking orders to products    |
| `payments`     | Payment records per order                |

### Entity Relationship

```
customers ──< orders ──< order_items >── products >── categories
                  └──< payments
```

---

## ⚙️ Setup Instructions

### Prerequisites
- MySQL 8.0+ installed
- MySQL Workbench or any MySQL client (DBeaver, CLI, etc.)

### Steps

```bash
# 1. Clone or download this project
git clone https://github.com/your-username/ecommerce-sql.git
cd ecommerce-sql

# 2. Open MySQL and run the files in order
mysql -u root -p < schema.sql
mysql -u root -p ecommerce_db < seed_data.sql
```

Or run manually in MySQL Workbench:
1. Open `schema.sql` → Execute
2. Open `seed_data.sql` → Execute
3. Open `queries.sql` → Run queries one by one

---

## 🧪 Concepts Covered

| Concept                  | Used In                                  |
|--------------------------|------------------------------------------|
| DDL (CREATE, ALTER)      | Schema setup                             |
| DML (INSERT, UPDATE)     | Seed data & trigger                      |
| INNER / LEFT JOIN        | Multi-table queries                      |
| GROUP BY + HAVING        | Aggregated reports                       |
| Subqueries               | Nested filtering                         |
| VIEW                     | `order_summary` reusable query           |
| TRIGGER                  | Auto stock reduction on order insert     |
| Window Functions (RANK)  | Customer spending leaderboard            |
| ENUM / FOREIGN KEY       | Data integrity constraints               |

---

## 📊 Sample Queries

### Total Revenue per Customer
```sql
SELECT c.full_name, SUM(oi.quantity * oi.unit_price) AS total_spent
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
JOIN order_items oi ON o.order_id = oi.order_id
GROUP BY c.customer_id
ORDER BY total_spent DESC;
```

### Top 3 Best-Selling Products
```sql
SELECT p.product_name, SUM(oi.quantity) AS total_sold
FROM products p
JOIN order_items oi ON p.product_id = oi.product_id
GROUP BY p.product_id
ORDER BY total_sold DESC
LIMIT 3;
```

### Orders with Missing Payments (Unpaid)
```sql
SELECT o.order_id, c.full_name, o.status
FROM orders o
JOIN customers c ON o.customer_id = c.customer_id
LEFT JOIN payments p ON o.order_id = p.order_id
WHERE p.payment_id IS NULL;
```

---

## 🎯 Challenge Tasks

Try solving these independently:

- [ ] Customers who have **never placed an order** (`LEFT JOIN` + `IS NULL`)
- [ ] Products that have **never been ordered**
- [ ] Month with the **highest total revenue**
- [ ] Rank customers by spending using **`RANK()` window function**
- [ ] Orders where **payment is missing**

---

## 🛠️ Tech Stack

- **Database:** MySQL 8.0
- **Tools:** MySQL Workbench / DBeaver / MySQL CLI

---

## 👨‍💻 Author

**Balakrishna**
B.Tech Mechanical Engineering | Aspiring Data/Software Engineer
[GitHub](https://github.com/balakrishnavelamala339)

---

## 📄 License

This project is open-source and free to use for learning purposes.

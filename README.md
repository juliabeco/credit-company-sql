# 💳 Credit Company Project

This SQL project simulates a simplified credit company system, including clients, financial products, transactions, and payments. It aims to demonstrate relational database modeling, data population, and the execution of meaningful SQL queries using aggregation, filtering, and joins.

## 📁 Database Structure

The project creates a MySQL database named `credit_company` with the following normalized tables:

### 1. `clientes`
- `id_cliente` (Primary Key)
- `nombre`
- `fecha_nacimiento`
- `genero` (`M` or `F`)
- `ingresos_mensuales`
- `estado_civil`

### 2. `productos`
- `id_producto` (Primary Key)
- `nombre_producto`
- `tasa_de_interes` (percentage)
- `comision_apertura`
- `cuota_mensual`

### 3. `transacciones`
- `id_transaccion` (Primary Key)
- `id_cliente` (FK)
- `id_producto` (FK)
- `fecha_transaccion`
- `monto_transaccion`
- `tipo_transaccion` (`P` = Purchase, `A` = Additional)

### 4. `pagos`
- `id_pago` (Primary Key)
- `id_cliente` (FK)
- `id_transaccion` (FK)
- `monto_pago`
- `fecha_pago`

## 📊 Sample Data

The tables were populated with realistic data, including:
- 20 clients with diverse income levels, marital status, and genders.
- 4 financial products (personal loans, credit cards, and credit lines).
- 30 transactions simulating different types of operations.
- 30 corresponding payments.

All foreign keys were updated and validated to reflect relational integrity (e.g., `pagos.id_cliente` updated via `JOIN` with `transacciones`).

## 🔍 Key Queries and Insights

Here are some of the analytical queries included:

### ✔️ Total Transactions Per Client
Shows the number of transactions each customer has made.

```sql
SELECT id_cliente, COUNT(*) AS total_transacciones
FROM transacciones
GROUP BY id_cliente;
```

### ✔️ Total Amount Transacted Per Product
Summarizes total amount per financial product.

```sql
SELECT id_producto, SUM(monto_transaccion) AS total_monto
FROM transacciones
GROUP BY id_producto;
```

### ✔️ Customers with More Than One Product
Identifies clients with a diversified product portfolio.

```sql
SELECT c.nombre, COUNT(DISTINCT t.id_producto) AS productos_contratados
FROM clientes c
JOIN transacciones t ON c.id_cliente = t.id_cliente
GROUP BY c.id_cliente
HAVING COUNT(DISTINCT t.id_producto) > 1;
```

### ✔️ Average Monthly Income by Product
Explores income profiles of clients by product usage.

```sql
SELECT pr.nombre_producto, 
       ROUND(AVG(c.ingresos_mensuales), 2) AS avg_income
FROM transacciones t
JOIN productos pr ON t.id_producto = pr.id_producto
JOIN clientes c ON t.id_cliente = c.id_cliente
GROUP BY pr.nombre_producto;
```

## 📌 Skills Highlighted

- SQL database design and normalization
- Data integrity and foreign key relationships
- Data aggregation and grouping
- Filtering with `HAVING` and `JOIN`
- Realistic data simulation

## 🛠️ Tools Used

- MySQL
- SQL (DDL & DML)
- SQL queries for analytics and data quality control

## 📚 Use Cases

This dataset and structure can be used to:

- Simulate loan behavior
- Analyze customer profiles
- Calculate average payments, product penetration, or default patterns (future extensions)

---

✅ **Status**: Project completed  
👤 Author: **Julia Becaria Coquet**

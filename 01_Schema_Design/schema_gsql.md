# Schema Design using GSQL

## 🔹 1. Connect to GSQL

First, enter your container:

```bash
docker exec -it tigergraph bash
```

Then launch the GSQL shell:

```bash
gsql
```

---

## 🔹 2. Global Context

Always start schema design with **global mode**:

```gsql
USE GLOBAL
```

This allows you to define vertices, edges, and graphs.

---

## 🔹 3. Dropping Old Schema (Optional)

Before creating a fresh schema, you may want to drop existing ones.

- Drop an **edge**:

```gsql
DROP EDGE placed
```

- Drop a **vertex**:

```gsql
DROP VERTEX Customer
```

---

## 🔹 4. Creating Vertices

Define entities as **vertices**.
Each vertex needs a **PRIMARY_ID** and can have attributes.

```gsql
CREATE VERTEX Customer (
  PRIMARY_ID customer_id STRING,
  name STRING,
  email STRING
)

CREATE VERTEX Order (
  PRIMARY_ID order_id STRING,
  date DATETIME,
  amount FLOAT
)

CREATE VERTEX Product (
  PRIMARY_ID product_id STRING,
  name STRING,
  price FLOAT
)
```

---

## 🔹 5. Creating Edges

Edges represent **relationships** between vertices.

```gsql
CREATE DIRECTED EDGE placed (FROM Customer, TO Order)

CREATE DIRECTED EDGE contains (FROM Order, TO Product)
```

- `DIRECTED` → one-way relationship (e.g., Customer → Order).
- `UNDIRECTED` → two-way relationship (e.g., friendship).

---

## 🔹 6. Creating the Graph

Finally, bundle everything into a **graph** object.

```gsql
CREATE GRAPH ecommerceGraph(
  Customer,
  Order,
  Product,
  placed,
  contains
)
```

This graph now knows which vertices and edges belong together.

---

## 🔹 7. Example Workflow

Here’s the **full minimal schema file** (`schema.gsql`):

```gsql
USE GLOBAL

DROP GRAPH ecommerceGraph

DROP EDGE placed
DROP EDGE contains

DROP VERTEX Customer
DROP VERTEX Order
DROP VERTEX Product

CREATE VERTEX Customer (
  PRIMARY_ID customer_id STRING,
  name STRING,
  email STRING
)

CREATE VERTEX Order (
  PRIMARY_ID order_id STRING,
  date DATETIME,
  amount FLOAT
)

CREATE VERTEX Product (
  PRIMARY_ID product_id STRING,
  name STRING,
  price FLOAT
)

CREATE DIRECTED EDGE placed (FROM Customer, TO Order)
CREATE DIRECTED EDGE contains (FROM Order, TO Product)

CREATE GRAPH ecommerceGraph(Customer, Order, Product, placed, contains)
```

Run this inside GSQL:

```bash
gsql schema.gsql
```

---

## 🔹 8. Next Steps

- **Create a loading job** (`LOAD` statements) to load data from CSV into these vertices/edges.
- **Access GraphStudio** (GUI) at:
  👉 [http://localhost:14240](http://localhost:14240)

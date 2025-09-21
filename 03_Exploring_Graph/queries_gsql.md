# TG GSQL Queries

```sql
SELECT c FROM (c:Customers) ORDER BY c.customer_id
```
-----
```sql
SELECT r
FROM (c:Customers)-[:WRITES_REVIEW]->(r:Reviews)
WHERE c.customer_id == 1
ORDER BY r.review_id;
```
-----
```sql
SELECT r.review_text, p.product_id, p.product_description
FROM (c:Customers)-[:WRITES_REVIEW]->(r:Reviews) <- [:HAS_REVIEW]-(p:Products)
WHERE c.customer_id == 1;
```
-----
```sql
SELECT c, r, e
FROM (c:Customers)-[e:WRITES_REVIEW]->(r:Reviews)
WHERE c.customer_id == 1;
```
-----
```sql
SELECT c,r,p,e1,e2
FROM (c:Customers)-[e1:WRITES_REVIEW]->(r:Reviews) <- [e2:HAS_REVIEW]-(p:Products)
WHERE c.customer_id == 1;
```
-----
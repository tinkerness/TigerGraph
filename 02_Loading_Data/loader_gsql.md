sample code to load vertices:

```sql
USE GRAPH RetailGraph

CREATE LOADING JOB load_vertices FOR GRAPH RetailGraph {

    DEFINE FILENAME fcustomers = "/home/tigergraph/tiger_csvs/customers.csv";

    LOAD fcustomers TO VERTEX Customers VALUES (
        $"customer_id", $"first_name", $"last_name", $"email", $"address", $"city", $"state", $"zip_code", $"country"
    ) USING SEPARATOR=",", HEADER="true";

    // -- Incase a field contains comma separated values like address enclosed within quotes add QUOTE="double" / "single"
    // -- eg: USING SEPARATOR=",", HEADER="true", QUOTE="double";

    }
```

copy file to docker container:

```bash
docker cp loader.gsql tigergraph:/home/tigergraph/db_files/loader.gsql
```

run the file using:

```bash
gsql loader.gsql
```

in gsql shell:

```bash
USE GRAPH RetailGraph
RUN LOADING JOB load_vertices
```

repeat same for egdes:

```bash
docker cp edge_loader.gsql tigergraph:/home/tigergraph/db_files/edge_loader.gsql
```

```bash
gsql edge_loader.gsql
```

in gsql shell:

```bash
USE GRAPH RetailGraph
RUN LOADING JOB load_edges
```

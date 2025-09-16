- copy files:

```bash
docker cp schema.gsql tg_container:/home/tigergraph/schema.gsql
```

`# Note`: Replace `tg_container` with name of container. Eg:

```bash
docker cp schema.gsql tigergraph:/home/tigergraph/db_files/schema.gsql
```

- To run the file:
  Switch to gsql shell:

```bash
gsql /home/tigergraph/db_files/schema.gsql
```

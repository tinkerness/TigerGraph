# TigerGraph

# Installation

### Download the TigerGraph community edition Docker image

### Make sure Docker Desktop is running

verify by running in terminal/PowerShell:

```
docker --version
```

### Load the TigerGraph Docker image

```
docker load -i tigergraph-4.2.0-community-docker-image.tar.gz
```

`# NOTE:` verify file location before running. eg: `docker load -i D:\downloads\tigergraph-4.2.0-community-docker-image.tar.gz`

After it finishes, confirm it’s there:

```
docker images
```

### Run the TigerGraph container

```
docker run -d -p 14022:22 -p 9000:9000 -p 14240:14240 --name tigergraph --ulimit nofile=1000000:1000000 -v tg-data:/home/tigergraph tigergraph/community:4.2.0
```

Explanation of ports:

- 14022 → SSH access to the container
- 9000 → REST++ API (query endpoint)
- 14240 → GraphStudio (web UI for TigerGraph)

`NOTE:` To reuse the existing container instead of creating a new one:

```
docker start tigergraph
```

After running, check container status:

```
docker ps
```

### Access TigerGraph services

- Inside container:

```
docker exec -it tigergraph bash
```

start the tiger graph services

```
gadmin start all
```

verify services are running

```
gadmin status
```

GSQL shell:

```
gsql
```

- GraphStudio (GUI): Open [http://localhost:14240](http://localhost:14240) in your browser.

  - Default login:
    - Username: `tigergraph`
    - Password: `tigergraph`

- REST API test: [http://localhost:9000/echo](http://localhost:9000/echo)

```
curl http://localhost:9000/echo
```

## Next Steps

- **Design Schema** based on given data.
  [01_Schema_Design](.\01_Schema_Design\schema_gsql.md)

- **Access GraphStudio** (GUI) at:
  👉 [http://localhost:14240](http://localhost:14240)

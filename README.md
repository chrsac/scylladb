# Deploy scylladb Docker with 3 nodes
### ScyllaDB Docker 

![diagram_Docker](https://github.com/chrsac/scylladb/assets/8300074/8e3bbfd1-a1e2-4f60-96c9-364e708eda35)

## Create DataDir Directory

```bash
mkdir -p /var/lib/scylla
```

## Add First Node 

```bash
docker run -d --name scylla-node1  \
  -p 7000:7000 -p 7001:7001 -p 7199:7199 -p 9042:9042 -p 9160:9160 \
  --mount type=bind,source=/var/lib/scylla,destination=/var/lib/scylla \
  sb3:5000/scylla:latest \
  --smp 2 --memory 2G --overprovisioned 1 \
  --broadcast-rpc-address 192.168.1.1  --broadcast-address 192.168.1.1 \
  --seeds 192.168.1.1

```

## run: 

```bash
   docker exec -it scylla-node1  bash
```

```bash
   root@585a590e56e8:/# nodetool status
```

```console
  Datacenter: datacenter1
=======================
Status=Up/Down
|/ State=Normal/Leaving/Joining/Moving
--  Address         Load       Tokens       Owns    Host ID                               Rack
UN  x.x.x.x         193.15 KB  256          ?       dbfdfde7-f072-427a-9452-cb07d121a0e5  rack1

```

## Add node 2 and other nodes

Change --broadcast-rpc-address and --broadcast-address with VM IP Address.

```bash
docker run -d --name scylla-node1  \
  -p 7000:7000 -p 7001:7001 -p 7199:7199 -p 9042:9042 -p 9160:9160 \
  --mount type=bind,source=/var/lib/scylla,destination=/var/lib/scylla \
  sb3:5000/scylla:latest \
  --smp 2 --memory 2G --overprovisioned 1 \
  --broadcast-rpc-address 192.168.1.2  --broadcast-address 192.168.1.2 \
  --seeds 192.168.1.1
```






  



# Citus-Operator

## Run postgresql cluster on localhost

```bash
$ sudo mkdir -p /opt/data/haproxy /opt/data/prometheus-data /opt/data/stolon-data0 /opt/data/stolon-data1 /opt/data/stolon-data2
$ sudo cp haproxy.cfg pgpass /opt/data/haproxy
$ sudo cp *.yml cluster_spec.json *_env.txt /opt/data
$ cd /opt/data
$ sudo docker-compose up -d
# initialize cluster spec in etcd
$ /usr/local/bin/stolonctl --cluster-name stolon-cluster --store-backend=etcdv3 init -f /opt/data/cluster_spec.json

# connect to master node
$ psql --host=127.0.0.1 --port=5440 --username=postgres
postgres=# SELECT inet_server_addr(), inet_server_port(), pg_is_in_recovery(), inet_client_port();

# connect to one of standby nodes
$ psql --host=127.0.0.1 --port=5441 --username=postgres
postgres=# SELECT inet_server_addr(), inet_server_port(), pg_is_in_recovery(), inet_client_port();
```

## Reference
- https://github.com/citusdata/docker/ generates the latest official citus image.
- https://github.com/sorintlab/stolon/ Postgresql HA
- https://github.com/haproxytech/dataplaneapi haproxy management api

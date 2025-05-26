


```
docker exec -it es-cluster-es01-1 cat /usr/share/elasticsearch/config/certs/ca/ca.crt > C:\Elastic\ca.crt
.\elastic-agent.exe install --url=https://fleet-server:8220 --enrollment-token=ZmhwaDFaWUJzSkx1UnFhcm4ydXk6OXVEdWNibDBST3FWaGRWaGhfNmFJQQ== -a C:\Elastic\ca.crt
```

```
docker exec -it es-cluster-osquery-1 bash

```


```
docker run --name zeek-linux --host zeek-linux --network elastic-package-stack_default --rm --mount type=bind,src=C:\Users\arnol\Desktop\elastic-stack\examples\raw_sample_log_dataset\Zeek,dst=/var/log/bro/current --env FLEET_CA=elastic-CA.crt --env FLEET_ENROLL=1 --env FLEET_URL=https://fleet-server:8220 --env FLEET_ENROLLMENT_TOKEN=SDhJcGtKWUJsTzNkYVF0ZEFiZ1o6c0NGNVZLX1hSYUNORjVmbDFfNUNQQQ== docker.elastic.co/elastic-agent/elastic-agent-wolfi:8.17.4yes

```
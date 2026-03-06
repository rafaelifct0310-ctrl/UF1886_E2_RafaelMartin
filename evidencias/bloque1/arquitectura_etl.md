# Arquitectura

### Contenedores activos

##### comando:
```
docker ps --format "table {{.Names}}\t{{.Image}}\t{{.Ports}}\t{{.Status}}"
```

```
NAMES         IMAGE                PORTS                                                                                      STATUS
odoo.18       odoo:18.0            0.0.0.0:8001->8069/tcp, [::]:8001->8069/tcp, 0.0.0.0:8002->8072/tcp, [::]:8002->8072/tcp   Up 40 minutes
postgres.db   postgres:16-alpine   0.0.0.0:5432->5432/tcp, [::]:5432->5432/tcp                                                Up 40 minutes
```
### Network
##### comando:
```
docker network ls
```

```
NETWORK ID     NAME                   DRIVER    SCOPE
6a5d88b9d36a   uf1886_e2_rm_default   bridge    local
```

### Volume

##### comando:
```
docker volume ls
```
 ```
 DRIVER    VOLUME NAME
 local     uf1886_e2_rm_odoo-db-data
 local     uf1886_e2_rm_odoo-web-data
```
### Recursos del host

```
DeviceID Name                                           Caption
-------- ----                                           -------
CPU0     11th Gen Intel(R) Core(TM) i5-1135G7 @ 2.40GHz Intel64 Family 6 Model...


TotalVisibleMemorySize FreePhysicalMemory
---------------------- ------------------
              16507808            6568812
```

### Arquitectura lógica
##### comando:
```
docker port odoo.18
```
```
8069/tcp -> 0.0.0.0:8001
8069/tcp -> [::]:8001
8072/tcp -> 0.0.0.0:8002
8072/tcp -> [::]:8002
```
```
docker port postgres.db
```
```
5432/tcp -> 0.0.0.0:5432
5432/tcp -> [::]:5432
```
### Confirmar Apache Hop está en el host
```
hop-conf.bat -v
```
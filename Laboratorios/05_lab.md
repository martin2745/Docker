# Laboratorios Curso Docker

### Nombre: Martín

### Apellidos: Gil Blanco

---

### **Laboratorio 1: Curso Docker**

#### **1. Comando para parar todos los contenedores**

```bash
docker stop $(docker ps -q)
```

```bash
PS C:\Users\gilbl\OneDrive\Escritorio\Martin\Trabajo\2024-2025\Ordinario\Diseño de Interfaces\Docker> docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS                    NAMES
2d99af97a4c9   mariadb   "docker-entrypoint.s…"   8 seconds ago   Up 8 seconds   0.0.0.0:3307->3306/tcp   bd1

PS C:\Users\gilbl\OneDrive\Escritorio\Martin\Trabajo\2024-2025\Ordinario\Diseño de Interfaces\Docker> docker stop $(docker ps -q)
2d99af97a4c9
```

#### **2. Comando para eliminar todos los contenedores**

```bash
docker rm $(docker ps -aq)
```

```bash
PS C:\Users\gilbl\OneDrive\Escritorio\Martin\Trabajo\2024-2025\Ordinario\Diseño de Interfaces\Docker> docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS                     PORTS     NAMES
2d99af97a4c9   mariadb   "docker-entrypoint.s…"   21 seconds ago   Exited (0) 7 seconds ago             bd1

PS C:\Users\gilbl\OneDrive\Escritorio\Martin\Trabajo\2024-2025\Ordinario\Diseño de Interfaces\Docker> docker rm $(docker ps -aq)
2d99af97a4c9
```

#### **3. Lanzar un contenedor llamado `web1` con la imagen `agarciaf/intranet`**

```bash
docker run -d --name web1 agarciaf/intranet
```

```bash
PS C:\Users\gilbl\OneDrive\Escritorio\Martin\Trabajo\2024-2025\Ordinario\Diseño de Interfaces\Docker> docker run -d --name web1 agarciaf/intranet
Unable to find image 'agarciaf/intranet:latest' locally
latest: Pulling from agarciaf/intranet
a3ed95caeb02: Pull complete
35d9d5d11536: Pull complete
c422cdb256a9: Pull complete
bd3dfdafe65b: Pull complete
bd3462764183: Pull complete
665c411390e3: Pull complete
8fc0c0a1c4fe: Pull complete
bc31532139f0: Pull complete
555193311939: Pull complete
50197e4977e2: Pull complete
11cf2fa9714b: Pull complete
88d7e466811c: Pull complete
6969966ecc41: Pull complete
f99014094379: Pull complete
31ec0d0094d4: Pull complete
54cfd34f58b8: Pull complete
f8c1adcda761: Pull complete
Digest: sha256:a6c66644ee7547ea2f17de07dc67f11307b469fe5c9002dfc38433bad5f269c5
Status: Downloaded newer image for agarciaf/intranet:latest
a5921babd57b236b0bb94917628580fc2cea9d793d4c3bd18b896a5ce9778387

PS C:\Users\gilbl\OneDrive\Escritorio\Martin\Trabajo\2024-2025\Ordinario\Diseño de Interfaces\Docker> docker ps -a
CONTAINER ID   IMAGE               COMMAND            CREATED         STATUS                       PORTS     NAMES
a5921babd57b   agarciaf/intranet   "supervisord -n"   9 seconds ago   Exited (139) 7 seconds ago             web1
```

#### **4. Lanzar un contenedor llamado `bd1` con la imagen `mariadb`**

```bash
docker container run `
 --name bd1 `
 -dp 3307:3306 `
 -e MARIADB_USER=example-user `
 -e MARIADB_PASSWORD=user-password `
 -e MARIADB_ROOT_PASSWORD=root-secret-password `
 -e MARIADB_DATABASE=world-db `
 mariadb
```

```bash
PS C:\Users\gilbl\OneDrive\Escritorio\Martin\Trabajo\2024-2025\Ordinario\Diseño de Interfaces\Docker> docker container run `
>>  --name bd1 `
>>  -dp 3307:3306 `
>>  -e MARIADB_USER=example-user `
>>  -e MARIADB_PASSWORD=user-password `
>>  -e MARIADB_ROOT_PASSWORD=root-secret-password `
>>  -e MARIADB_DATABASE=world-db `
>>  mariadb
e653ed202377bb56c7b3d3982db452dbe7e9895dd67512dc43ce764d49565c80

PS C:\Users\gilbl\OneDrive\Escritorio\Martin\Trabajo\2024-2025\Ordinario\Diseño de Interfaces\Docker> docker ps -a
CONTAINER ID   IMAGE               COMMAND                  CREATED          STATUS                        PORTS                    NAMES
e653ed202377   mariadb             "docker-entrypoint.s…"   6 seconds ago    Up 5 seconds                  0.0.0.0:3307->3306/tcp   bd1
a5921babd57b   agarciaf/intranet   "supervisord -n"         54 seconds ago   Exited (139) 52 seconds ago                            web1
```

#### **5. Lanzar un contenedor llamado `bd2` con la imagen `postgres`**

```bash
docker container run `
 -d `
 --name postgres-db `
 -e POSTGRES_PASSWORD=123456 `
 -v postgres-db:/var/lib/postgresql/data `
 postgres:15.1
```

```bash
PS C:\Users\gilbl\OneDrive\Escritorio\Martin\Trabajo\2024-2025\Ordinario\Diseño de Interfaces\Docker> docker container run `
>>  -d `
>>  --name postgres-db `
>>  -e POSTGRES_PASSWORD=123456 `
>>  -v postgres-db:/var/lib/postgresql/data `
>> postgres
0b01ab2aa2a7effcc5c9f34253a4429960a97d18baf9f867445b3f45f42e6958

PS C:\Users\gilbl\OneDrive\Escritorio\Martin\Trabajo\2024-2025\Ordinario\Diseño de Interfaces\Docker> docker ps -a
CONTAINER ID   IMAGE               COMMAND                  CREATED          STATUS                       PORTS                    NAMES
0b01ab2aa2a7   postgres            "docker-entrypoint.s…"   11 seconds ago   Up 10 seconds                5432/tcp                 postgres-db
e653ed202377   mariadb             "docker-entrypoint.s…"   2 minutes ago    Up 2 minutes                 0.0.0.0:3307->3306/tcp   bd1
a5921babd57b   agarciaf/intranet   "supervisord -n"         2 minutes ago    Exited (139) 2 minutes ago                            web1
```

#### **6. Lanzar un contenedor llamado `web2` que exponga el puerto en nuestra máquina `81` basado en la imagen `nginx`, y que se reinicie siempre**

```bash
docker run -d --name web2 -p 81:80 --restart always nginx
```

```bash
PS C:\Users\gilbl\OneDrive\Escritorio\Martin\Trabajo\2024-2025\Ordinario\Diseño de Interfaces\Docker> docker run -d --name web2 -p 81:80 --restart always nginx
e5f23df51d9aed5c7c0da913247150759766db5c12f09d4b19754dbf4f743ca7

PS C:\Users\gilbl\OneDrive\Escritorio\Martin\Trabajo\2024-2025\Ordinario\Diseño de Interfaces\Docker> docker ps -a
CONTAINER ID   IMAGE               COMMAND                  CREATED              STATUS                       PORTS                    NAMES
e5f23df51d9a   nginx               "/docker-entrypoint.…"   59 seconds ago       Up 58 seconds                0.0.0.0:81->80/tcp       web2
0b01ab2aa2a7   postgres            "docker-entrypoint.s…"   About a minute ago   Up About a minute            5432/tcp                 postgres-db
e653ed202377   mariadb             "docker-entrypoint.s…"   3 minutes ago        Up 3 minutes                 0.0.0.0:3307->3306/tcp   bd1
a5921babd57b   agarciaf/intranet   "supervisord -n"         4 minutes ago        Exited (139) 4 minutes ago                            web1
```

#### **7. ¿Qué IP tienen los contenedores `web1` y `web2`?**

Con el siguiente comando podemos ver el estado y buscar el apartado `"IPAddress": "X.X.X.X"`, donde están las IPs como `"172.17.0.2"`.

```bash
docker inspect id_contenedor/nombre_contenedor
```

```bash
PS C:\Users\gilbl\OneDrive\Escritorio\Martin\Trabajo\2024-2025\Ordinario\Diseño de Interfaces\Docker> docker inspect web2
"IPAddress": "172.17.0.4",

PS C:\Users\gilbl\OneDrive\Escritorio\Martin\Trabajo\2024-2025\Ordinario\Diseño de Interfaces\Docker> docker inspect web1
"IPAddress": "172.17.0.5",
```

#### **8. Comando para ver las estadísticas del contenedor `web1` y `web2`**

```bash
docker stats
```

```docker
CONTAINER ID   NAME      CPU %     MEM USAGE / LIMIT     MEM %     NET I/O     BLOCK I/O   PIDS
e5f23df51d9a   web2      0.00%     10.01MiB / 7.441GiB   0.13%     746B / 0B   0B / 0B     13
```

---

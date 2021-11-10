# Docker

<aside>
💡 Crie sua conta no Docker Hub e no PWD

</aside>

[Docker Hub Container Image Library | App Containerization](https://hub.docker.com/)

[Play with Docker](https://labs.play-with-docker.com/)

---

[percurso de aprendizado docker](https://dockerlabs.collabnix.com/workshop/docker/)

<aside>
💡 Imagens

</aside>

```bash
docker pull alpine:3.6
docker pull alpine:3.7
```

```bash
docker images
```

<aside>
💡 Containers

</aside>

```bash
docker run -d -p 80:80 nginx
```

```bash
docker ps -a
```

<aside>
💡 Exportando e importando containeres como imagens

</aside>

```bash
docker export <container> > <filename>.tar
```

```bash
docker import - mynginx < <filename>.tar
```

<aside>
💡 Ou, exportando e importando imagens

</aside>

```bash
docker save -o mynginx1.tar nginx
```

```bash
docker load < mynginx1.tar
```

<aside>
💡 Subindo uma imagem para o DockerHub

</aside>

```bash
docker run -dit alpine sh
```

```bash
docker exec -it /bin/sh
```

```bash
cat /etc/os-release
```

<aside>
💡 Modificar o container

</aside>

```bash
docker commit -m "Alpine Python 3" <container> <usuario>/<repo>
```

```bash
docker login
```

```bash
docker push <usuario>/repo
```

---

## Dockerfiles...

- ADD
- COPY
- CMD
- ENTRYPOINT
- RUN
- WORKDIR
- ENV

[Docker Hub](https://hub.docker.com/r/bitnami/mariadb)

---

<aside>
💡 Docker Compose!!

</aside>

```yaml
version: '2'
services:
  mysql:
    image: 'bitnami/mariadb'
    ports: 
      - '3306:3306'
    environment:
      - MARIADB_ROOT_PASSWORD=secret

  phpmyadmin:
    image: 'phpmyadmin/phpmyadmin'
    links:
      - mysql
    ports:
      - '80:80'
    environment:
      PMA_HOST: mysql
      PMA_PORT: 3306
```

<aside>
💡 O que mais?

</aside>

## Docker Swarm!

Docker Engine 1.12

```bash
docker swarm init
```

```bash
docker swarm init --advertise-addr eth0
```

```bash
version: '3'
services:
  mysql:
    image: 'bitnami/mariadb'
    deploy:
      mode: replicated
      replicas: 2
      resources:
        limits:
          cpus: '0.25'
          memory: '512M'
        reservations:
          cpus: '0.2'
          memory: '256M'
    networks:
      - exemplo_net
    environment:
      - MARIADB_ROOT_PASSWORD=secret
phpmyadmin:
    image: 'phpmyadmin/phpmyadmin'
    networks:
      - exemplo_net
    deploy:
      mode: replicated
      resources:
        limits:
          cpus: '0.25'
          memory: 512M
        reservations:
          cpus: '0.25'
    links:
      - mysql
    ports:
      - '80:80'
    environment:
      PMA_HOST: mysql
      PMA_PORT: 3306

networks:
  exemplo_net:
```

```bash
docker stack deploy --compose-file docker-compose.yml stackdemo
```

[Docker Hub](https://hub.docker.com/r/linuxserver/sonarr)

[Docker Hub](https://hub.docker.com/r/linuxserver/lidarr)

[Docker Hub](https://hub.docker.com/r/linuxserver/radarr)

[Docker Hub](https://hub.docker.com/r/linuxserver/plex)

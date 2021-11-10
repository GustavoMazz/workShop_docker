# Docker

<aside>
💡 O que é o Docker?

</aside>

![Untitled](Docker%20f9049249acc44ecaa289e8dff0378c7e/Untitled.png)

<aside>
💡 Parece familiar? às vezes precisamos desprender muito tempo e energia intelectual para incluir um software que não se encaixa perfeitamente com outras aplicações, para que tudo seja carregado, enviado e vendido em outro lugar...

</aside>

![Untitled](Docker%20f9049249acc44ecaa289e8dff0378c7e/Untitled%201.png)

<aside>
💡 Crie sua conta no Docker Hub e no PWD

</aside>

[Docker Hub Container Image Library | App Containerization](https://hub.docker.com/)

[Play with Docker](https://labs.play-with-docker.com/)

<aside>
💡 **Antes dos containers**

</aside>

![https://hub.packtpub.com/wp-content/uploads/2018/03/skill-up-blog_2.png](https://hub.packtpub.com/wp-content/uploads/2018/03/skill-up-blog_2.png)

![Untitled](Docker%20f9049249acc44ecaa289e8dff0378c7e/Untitled%202.png)

## Quais variáveis se importar em um ambiente?

- Performance
- Escalabilidade
- Portabilidade
- Custo
- Segurança
- Habilidades existentes

![Untitled](Docker%20f9049249acc44ecaa289e8dff0378c7e/Untitled%203.png)

---

# Não confunda VMs com containers!

![https://eadn-wc03-4064062.nxedge.io/cdn/wp-content/uploads/2020/05/2020_05_13_12_19_07_PowerPoint_Slide_Show_Azure_AZ104_M01_Compute_ed1_.png](https://eadn-wc03-4064062.nxedge.io/cdn/wp-content/uploads/2020/05/2020_05_13_12_19_07_PowerPoint_Slide_Show_Azure_AZ104_M01_Compute_ed1_.png)

## Desenvolvedores - Dev

- Docker para Mac
- Docker para Windows
- Nativo para o Linux

## Operação - Ops

- Docker para AWS

[Amazon CloudWatch - Monitoramento de aplicativos e infraestrutura](https://aws.amazon.com/pt/cloudwatch/)

- Docker para Azure

---

<aside>
💡 Microserviços

</aside>

![microservice-1.gif](Docker%20f9049249acc44ecaa289e8dff0378c7e/microservice-1.gif)

<aside>
💡 Docker containers aumentam a flexibilidade e a performance

</aside>

[e4dd70ac-b365-49a1-b138-7c9e81e4672b-6.webp](Docker%20f9049249acc44ecaa289e8dff0378c7e/e4dd70ac-b365-49a1-b138-7c9e81e4672b-6.webp)

# Resumindo...

---

[GitHub - GustavoMazz/workShop_docker](https://github.com/GustavoMazz/workShop_docker)

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
docker run -d -p 80:80 alpine:3.6
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
apk update
```

```bash
apk add --no-cache python3 py3-pip
```

```bash
docker commit -m "Alpine Python 3" <container> <imagem>
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

[Compose file version 3 reference](https://docs.docker.com/compose/compose-file/compose-file-v3/)

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

```bash
docker service ls
```

```bash
docker ps -a
```

[Docker Hub](https://hub.docker.com/r/linuxserver/sonarr)

[Docker Hub](https://hub.docker.com/r/linuxserver/lidarr)

[Docker Hub](https://hub.docker.com/r/linuxserver/radarr)

[Docker Hub](https://hub.docker.com/r/linuxserver/plex)
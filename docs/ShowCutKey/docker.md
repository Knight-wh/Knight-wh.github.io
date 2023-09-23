# Docker

>[dockerawesome-compose Awesome Docker Compose samples](https://github.com/docker/awesome-compose)

## general

`docker ps -a`

`docker image ls`

## basic

`docker build -t <image-name> .` 创建镜像。 `-t <image-name>` 命名镜像

`docker run -dp 3000:3000 <image-name>` 运行容器。`-d` 后台运行，`-p` 指定端口

`docker stop <container-id>` 停止容器。

`docker rm <container-id>` 删除容器。

`docker exec <container-id>` 访问容器。

eg:

`docker exec <container-id> cat /data.txt`

`docker exec -it <mysql-container-id> mysql -u root -p` `-it`

## docker compose

`docker compose up -d` `-d` 后台运行

`docker compose down` `--volumes` 删除生成的`volume`

`docker compose logs -f` `-f` 生成实时输出

### mount-compose

```yaml
services:
  app:
    image: node:18-alpine
    command: sh -c "yarn install && yarn run dev"
    ports:
      - 127.0.0.1:3000:3000
    working_dir: /app
    volumes:
      - ./:/app
    environment:
      MYSQL_HOST: mysql
      MYSQL_USER: root
      MYSQL_PASSWORD: secret
      MYSQL_DB: todos

  mysql:
    image: mysql:8.0
    volumes:
      - todo-mysql-data:/var/lib/mysql
    environment:
      MYSQL_ROOT_PASSWORD: secret
      MYSQL_DATABASE: todos

volumes:
  todo-mysql-data:
```

### mount-cli

`docker volume create todo-db`

`docker run -dp 3000:3000 --mount type=volume,src=todo-db,target=/etc/todos <image>`

`docker run -it --mount type=bind,src="$(pwd)",target=/src ubuntu bash`

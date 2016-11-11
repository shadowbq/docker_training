
## remove docker containers

```
fireball@chestnut ~ $ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
fireball@chestnut ~ $ docker ps -a
CONTAINER ID        IMAGE                     COMMAND                  CREATED             STATUS                       PORTS               NAMES
69f2629ab671        graylog2/server:2.1.0-3   "/docker-entrypoint.s"   34 minutes ago      Exited (143) 5 minutes ago                       fireball_graylog_1
3cf7358b00ae        mongo:3                   "/entrypoint.sh mongo"   50 minutes ago      Exited (0) 5 minutes ago                         fireball_mongo_1
27c9246b470a        elasticsearch:2           "/docker-entrypoint.s"   50 minutes ago      Exited (143) 5 minutes ago                       fireball_elasticsearch_1
fireball@chestnut ~ $ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
elasticsearch       2                   3429053f4435        11 days ago         344 MB
mongo               3                   092cc6fb995c        12 days ago         342.4 MB
graylog2/server     latest              58a2b309b960        7 weeks ago         619.3 MB
graylog2/server     2.1.0-3             699bfad95438        7 weeks ago         620.7 MB
fireball@chestnut ~ $ docker rm fireball_graylog_1
fireball_graylog_1
fireball@chestnut ~ $ docker rm fireball_mongo_1
fireball_mongo_1
fireball@chestnut ~ $ docker rm fireball_elasticsearch_1
fireball_elasticsearch_1
fireball@chestnut ~ $ docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

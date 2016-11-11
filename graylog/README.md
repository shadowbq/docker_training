## Config Volumes
``` 
fireball@chestnut ~ $ sudo su -
chestnut ~ # mkdir -p /graylog/config
chestnut ~ # mkdir -p /graylog/data
chestnut ~ # mkdir -p /graylog/data/mongo
chestnut ~ # mkdir -p /graylog/data/elasticsearch
chestnut ~ # mkdir -p /graylog/data/journal
chestnut ~ # chmod -R a+w /graylog
```

```
fireball@chestnut /graylog/config $ wget https://raw.githubusercontent.com/Graylog2/graylog2-images/2.1/docker/confi                                                                        g/graylog.conf
--2016-11-03 01:16:20--  https://raw.githubusercontent.com/Graylog2/graylog2-images/2.1/docker/config/graylog.conf
Resolving raw.githubusercontent.com... 151.101.32.133
Connecting to raw.githubusercontent.com|151.101.32.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 21526 (21K) [text/plain]
Saving to: 'graylog.conf'

graylog.conf                  100%[===============================================>]  21.02K  --.-KB/s    in 0.05s

2016-11-03 01:16:21 (401 KB/s) - 'graylog.conf' saved [21526/21526]

fireball@chestnut /graylog/config $ wget https://raw.githubusercontent.com/Graylog2/graylog2-images/2.1/docker/confi                                                                        g/log4j2.xml
--2016-11-03 01:16:23--  https://raw.githubusercontent.com/Graylog2/graylog2-images/2.1/docker/config/log4j2.xml
Resolving raw.githubusercontent.com... 151.101.32.133
Connecting to raw.githubusercontent.com|151.101.32.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1674 (1.6K) [text/plain]
Saving to: 'log4j2.xml'

log4j2.xml                    100%[===============================================>]   1.63K  --.-KB/s    in 0s

2016-11-03 01:16:23 (416 MB/s) - 'log4j2.xml' saved [1674/1674]

fireball@chestnut /graylog/config $ ls -la
total 52
drwxrwxrwx. 2 root       root        4096 Nov  3 01:16 .
drwxrwxrwx. 4 root       root        4096 Nov  3 01:13 ..
-rw-r--r--. 1 fireball fireball 21526 Nov  3 01:16 graylog.conf
-rw-r--r--. 1 fireball fireball  1674 Nov  3 01:16 log4j2.xml
```

## Docker Compose

Download

```
chestnut ~ # mkdir -p /opt/bin
chestnut ~ # curl -L https://github.com/docker/compose/releases/download/1.8.1/docker-compose-`uname -s`-`uname -m` >                                                                         /opt/bin/docker-compose
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   600    0   600    0     0   6516      0 --:--:-- --:--:-- --:--:--  7228
100 7798k  100 7798k    0     0   331k      0  0:00:23  0:00:23 --:--:--  351k
chestnut ~ # cd /opt/bin/
chestnut bin # chmod +x ./docker-compose
```
### compose

`fireball@chestnut ~ $ cat docker-compose.yml`

```yml
version: '2'
services:
  mongo:
    image: "mongo:3"
  elasticsearch:
    image: "elasticsearch:2"
    command: "elasticsearch -Des.cluster.name='graylog'"
  graylog:
      image: graylog2/server:2.1.0-3
      environment:
        GRAYLOG_PASSWORD_SECRET: Thisisalongstoryandmay1123haveABC
        GRAYLOG_ROOT_PASSWORD_SHA2: d09359b9516c61f5a764632a69a30adde59fcc80ec35120dbe243af34fcb0b40
        GRAYLOG_WEB_ENDPOINT_URI: http://10.4.1.106:9000/api
      depends_on:
       - mongo
       - elasticsearch
      ports:
       - "9000:9000"
```       

### Up

non-caches

```
fireball@chestnut ~ $ docker-compose up
Creating network "fireball_default" with the default driver
Pulling graylog (graylog2/server:2.1.0-3)...
2.1.0-3: Pulling from graylog2/server
fdd5d7827f33: Already exists
a3ed95caeb02: Already exists
0f35d0fe50cc: Already exists
44091295bce9: Already exists
a7df6b0e1928: Already exists
e3f5c6e4eb7c: Already exists
078144e1612b: Already exists
ff7dd9deb980: Already exists
dd6e7f62ef4b: Pull complete
ba2882e7a4b6: Pull complete
a26ddc0204fb: Pull complete
10cae0473a6f: Pull complete
11641452aafb: Pull complete
96f48f517cf8: Pull complete
Digest: sha256:df8bc3f3011479d74af6d2f0a346f084246991ebe6e03d35142ca0fe3a2dac60
Status: Downloaded newer image for graylog2/server:2.1.0-3
Creating fireball_mongo_1
Creating fireball_elasticsearch_1
Creating fireball_graylog_1
Attaching to fireball_mongo_1, fireball_elasticsearch_1, fireball_graylog_1
mongo_1          | 2016-11-03T01:37:29.840+0000 I CONTROL  [initandlisten] MongoDB starting : pid=1 port=27017 dbpath=                                                                        /data/db 64-bit host=97cbbe8a1824
mongo_1          | 2016-11-03T01:37:29.840+0000 I CONTROL  [initandlisten] db version v3.2.10
[..]
```

Cached

```
fireball@chestnut ~ $ docker-compose up
Creating fireball_mongo_1
Creating fireball_elasticsearch_1
Creating fireball_graylog_1
Attaching to fireball_elasticsearch_1, fireball_mongo_1, fireball_graylog_1
mongo_1          | 2016-11-03T02:52:51.507+0000 I CONTROL  [initandlisten] MongoDB starting : pid=1 port=27017 dbpath=/data/db 64-bit host=c5bf99a97f3d
mongo_1          | 2016-11-03T02:52:51.507+0000 I CONTROL  [initandlisten] db version v3.2.10
mongo_1          | 2016-11-03T02:52:51.507+0000 I CONTROL  [initandlisten] git version: 79d9b3ab5ce20f51c272b4411202710a082d0317
mongo_1          | 2016-11-03T02:52:51.507+0000 I CONTROL  [initandlisten] OpenSSL version: OpenSSL 1.0.1t  3 May 2016
mongo_1          | 2016-11-03T02:52:51.507+0000 I CONTROL  [initandlisten] allocator: tcmalloc
[..]
```

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

## Production

```
fireball@chestnut /etc/systemd/system $ docker ps
CONTAINER ID        IMAGE                     COMMAND                  CREATED             STATUS                  PORTS                                                                                                                           NAMES
542bf4f8d6ad        graylog2/server:2.1.0-3   "/docker-entrypoint.s"   56 minutes ago      Up Less than a second   0.0.0.0:514->514/tcp, 0.0.0.0:514->514/udp, 0.0.0.0:1514->1514/tcp, 0.0.0.0:9000->9000/tcp, 0.0.0.0:5555->5555/udp, 12900/tcp   fireball_graylog_1
0dc73f2219ee        elasticsearch:2           "/docker-entrypoint.s"   56 minutes ago      Up Less than a second   9200/tcp, 9300/tcp                                                                                                              fireball_elasticsearch_1
c5bf99a97f3d        mongo:3                   "/entrypoint.sh mongo"   56 minutes ago      Up Less than a second   27017/tcp     
```

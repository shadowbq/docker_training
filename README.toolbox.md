## Familiar Toolbox
Toolbox is in coreos is a priviledged container
```
$ which toolbox
/usr/bin/toolbox
```

```
fireball@chestnut ~ $ vi .toolboxrc
```

## Start toolbox
Fedora is default
```
fireball@chestnut ~ $ toolbox
latest: Pulling from library/fedora
2bf01635e2a0: Downloading [==>                                                ] 4.315 MB/72.88 MB
^C
```

Ubuntu 
```
fireball@chestnut ~ $ cat ~/.toolboxrc
TOOLBOX_DOCKER_IMAGE=ubuntu
TOOLBOX_DOCKER_TAG=16.04
TOOLBOX_USER=root
```

Start Toolbox

```
fireball@chestnut ~ $ toolbox
16.04: Pulling from library/ubuntu
6bbedd9b76a4: Pull complete
fc19d60a83f1: Pull complete
de413bb911fd: Pull complete
2879a7ad3144: Pull complete
668604fde02e: Pull complete
Digest: sha256:2d44ae143feeb36f4c898d32ed2ab2dffeb3a573d2d8928646dfc9cb7deb1315
Status: Downloaded newer image for ubuntu:16.04
d5fbd22b32285829c00b9e8c3a3fb25fbeec339283a2590f5ff8fd81bcea3648
fireball-ubuntu-16.04
Spawning container fireball-ubuntu-16.04 on /var/lib/toolbox/fireball-ubuntu-16.04.
Press ^] three times within 1s to kill container.
```

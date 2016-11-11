# Docker Tutorial

Ignore this repo.

It only contains notes from my stumbles on Docker / CoreOS

## Enable Docker Compose systemd service for coreos

```shell
$> sudo systemctl enable /etc/systemd/system/docker_compose.service
Created symlink /etc/systemd/system/default.target.wants/docker_compose.service → /etc/systemd/system/docker_compose.service.
fireball@chestnut /etc/systemd/system $ sudo systemctl status docker_compose.service
● docker_compose.service - Composer
   Loaded: loaded (/etc/systemd/system/docker_compose.service; enabled; vendor preset: disabled)
   Active: activating (auto-restart) since Thu 2016-11-03 03:49:14 UTC; 7s ago
  Process: 18436 ExecStop=/opt/bin/docker-compose -f /home/fireball/docker-compose.yml stop (code=exited, status=0/SUCCESS)
  Process: 18121 ExecStart=/opt/bin/docker-compose -f /home/fireball/docker-compose.yml up -d (code=exited, status=0/SUCCESS)
 Main PID: 18121 (code=exited, status=0/SUCCESS)
```

* http://www.ericluwj.com/2015/10/20/installing-docker-compose-in-coreos.html
* https://github.com/docker/compose/releases
* http://www.thegeekstuff.com/2012/01/rsyslog-remote-logging
* https://github.com/coreos/toolbox
* https://coreos.com/os/docs/latest/install-debugging-tools.html
* https://docs.docker.com/engine/admin/host_integration/
* http://trackless.ca/2015/12/21/docker-compose-meets-systemd/

# Installation Targets


Instead of older ways(circa '15) with '-g' use a simple modification in `/etc/docker/daemon.json`:
```
{
    "graph": "/mnt",
    "storage-driver": "overlay"
}
```
Despite the method you have to reload configuration and restart Docker:

```
sudo systemctl daemon-reload
sudo systemctl restart docker
```

To confirm that Docker was reconfigured:
```
docker info|grep "Docker Root Dir"
Output should look like this:
```

Data loop file: /mnt/devicemapper/devicemapper/data
Metadata loop file: /mnt/devicemapper/devicemapper/metadata


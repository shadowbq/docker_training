edit offline cloudconfig with proper IPs

(connect CD)
Boot to ROS.
sudo passwd rancher
scp cloudconfig over from offline
sudo ros install -c cloudconfig.yaml -d /dev/sda
reboot (disconnect CD)

sudo ros service up open-vm-tools

-------------------------------------

# Install Rancher 2.0 GUI (not ROS but on ROS)

## on guacamole..
mysql user db cattle on guacamole server 10.0.0.201
change mysql.conf to bind to 0.0.0.0 <restart mysql service>
u/pw: cattle / XXXX@......

## on docker-1
sudo docker run -d --restart=unless-stopped -p 8080:8080 rancher/server --db-host 10.0.0.201 --db-port 3306 --db-user cattle --db-pass 'XXXXXX' --db-name cattle

## Go to 10.0.0.130:8080 Browser

# Add Manager UI as a Worker
sudo docker run -e CATTLE_AGENT_IP="10.0.0.130"  --rm --privileged -v /var/run/docker.sock:/var/run/docker.sock -v /var/lib/rancher:/var/lib/rancher rancher/agent:v1.2.7 http://10.0.0.130:8080/v1/scripts/F97EAFEC9B39FE2766C7:1483142400000:R4be3vLfWSxSZeTgUzpnPdZLo

# Docker machine
## Install virtualBox on deepin
- [Debian-based Linux distributions](https://www.virtualbox.org/wiki/Linux_Downloads)

```bash
# Add the following line to your /etc/apt/sources.list. According to your distribution, replace '<mydist>' with 'artful', 'zesty', 'yakkety', 'xenial', 'trusty', 'stretch', 'jessie', or 'wheezy' (older versions of VirtualBox supported different distributions):
deb https://download.virtualbox.org/virtualbox/debian <mydist> contrib
# You can add these keys with
wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | sudo apt-key add -
wget -q https://www.virtualbox.org/download/oracle_vbox.asc -O- | sudo apt-key add -
# To install VirtualBox, do  |  
sudo apt-get update
sudo apt-get install virtualbox-5.2
```
## create a cluster
- create a couple of VMS , using the VirtualBox driver
```bash
#  enusure that you have installed Oracle VirtualBox
docker-machine create --driver virtualbox myvm1
docker-machine create --driver virtualbox myvm2
# list the vms and get their ip addr
docker-machine ls
# initialize the swarm and add nodes.
# send commands to VMS
docker-machine ssh
# instruct one machine to become a swarm manager with
docker swarm init
# So , ...
# Always run docker swarm init and docker swarm join with port 2377 (the swarm management port), or no port at all and let it take the default
docker-machine ssh myvm1 "docker swarm init --advertise-addr <myvm1-ip>:<port>"
# add a worker to this swarm
docker-machine ssh myvm2 "docker swarm join --token <token> <vm2-ip>:<port>"
# on the manager , view the nodes in the swarm
 docker-machine ssh myvm1 "docker node ls"
```
- Only swarm managers like `myvm1` execute Docker commands, workers are for capacity.
- Configure a `docker-machine` shell to the swarm manager.
```bash
$ docker-machine env myvm2
export DOCKER_TLS_VERIFY="1"
export DOCKER_HOST="tcp://192.168.99.101:2376"
export DOCKER_CERT_PATH="/home/bqzhu/.docker/machine/machines/myvm2"
export DOCKER_MACHINE_NAME="myvm2"
$ eval $(docker-machine env myvm2)
# Unsetting docker-machine shell variable settings
$ eval $(docker-machine env -u)
```
- tear down the stack with
```bash
docker stack rm getstartedlab
```

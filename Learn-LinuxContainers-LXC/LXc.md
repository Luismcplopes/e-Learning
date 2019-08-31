# more info
https://blog.simos.info/how-to-make-your-lxd-container-get-ip-addresses-from-your-lan/
https://blog.simos.info/how-to-make-your-lxd-containers-get-ip-addresses-from-your-lan-using-a-bridge/

Here is the iptables command. Set three parameters, and then change the $PORT to each port that needs to be opened.
`PORT=80 SERVER_IP=your_server_ip CONTAINER_IP=your_container_ip INTERFACE=your_server_network_interface sudo -E bash -c 'iptables -t nat -I PREROUTING -i $INTERFACE -p TCP -d $SERVER_IP --dport $PORT -j DNAT --to-destination $CONTAINER_IP:$PORT -m comment --comment "forward to network port"'`

Replace

PORT: the network port. In the example it shows port 80 (www).
SERVER_IP: the server’s IP address.
CONTAINER_IP: the container’s IP address (use lxc list to find it).
INTERFACE: the server network interface. Probably eth0 or something similar.

exemplos:
`PORT=8080 PROTO=tcp SERVER_IP=your_server_ip CONTAINER_IP=your_container_ip INTERFACE=your_server_network_interface sudo -E bash -c 'iptables -t nat -I PREROUTING -i $INTERFACE -p $PROTO -d $SERVER_IP --dport $PORT -j DNAT --to-destination $CONTAINER_IP:$PORT -m comment --comment "forward to Kodi network port 8080 TCP"' `

`PORT=9777 PROTO=udp SERVER_IP=your_server_ip CONTAINER_IP=your_container_ip INTERFACE=your_server_network_interface sudo -E bash -c 'iptables -t nat -I PREROUTING -i $INTERFACE -p $PROTO -d $SERVER_IP --dport $PORT -j DNAT --to-destination $CONTAINER_IP:$PORT -m comment --comment "forward to Kodi network port 8080 TCP"' `




# LXC -- Linux Containers
## Install 
`apt-get install lxc`
```
sudo -i
apt-get install lxc
lxc-ls --fancy
lxc-create -t ubuntu -n mycontainer -d
lxc-ls -f
lxc-start -n mycontainer -d
lxc-atach -n mycontainer
lxc-destroy
apt-get install python-minimal -no-install-recommends
logout
```
## Listar containers
`lxc-ls -f` ou `lxc-ls -f`
## Create a container (-t os type, -n container name)
`lxc-create -t ubuntu -n mycontainer`
## Start/Stop a container (-d detached, -n container name -k kill)
`lxc-stop -n mycontainer -k ` or `lxc-start -n mycontainer -d`
## limiter CPU on a container (grep processor /proc/cpuinfo)
`lxc config set mycontainer limits.cpu 1` 
## limiter Memory on a container 
`lxc config set mycontainer limits.memory 1 `
### Exec on a container
`lxc exec mycontainer bash`
### attach to a container
`lxc-attach -n mycontainer`
#### ssh to a container (default login/pass: ubuntu/ubuntu)
`ssh ubuntu@containerip`
#### exit the container
`logout` or `poweroff` or `shutdown -h now`
## Freeze a container
`lxc-freeze -n mycontainer` or `lxc-unfreeze -n mycontainer`
## take a snapshot form a container
`lxc snapshot mycontainer`
## view info from a container
`lxc info mycontainer`
## Restore a snapshot a container
`lxc restore mycontainer snapshot`
### Auto start (-L only list, -a all)
`lxc-autostart -L`
## Console
`lxc-console`
## Destroy a container
`lxc-destroy`
## Cache dir
`sudo ls /cache/lxc/`
## Container dir
`sudo ls /var/lib/lxc/`
## Copy to a container
`cp /things/ /var/lib/lxc/mycontainer/opt/things/`
## Templates 
`ls /usr/share/templates`


# Config
## Checkconfig
`lxc-checkconfig`
## Config file (syntax is "key = value")
`cat /var/lib/lxc/mycontainer/config`
```
#######eof#####
lxc.networking.ipv4 = 10.0.3.100/24 10.0.3.255 #(if dont change the intreface config its kippoing 2 IPs)
lxc.networking.ipv4.gateway = auto
lxc.start.auto = 1
lxc.start.delay = 15
lxc.start.order = 10
#lxc.group = infrastructure,dns #(if active the autostart dont work)
```
### More info
 - https://www.youtube.com/playlist?list=PLtK75qxsQaMLwF_uCB_CK8wIE17D-afuJ
 - https://stgraber.org/2013/12/20/lxc-1-0-blog-post-series/

# LXC LXD - Ansible
sudo apt install lxc-dev



# create a user and home directory
useradd -m -d /home/luisubu luisubu

# Create the .ssh subdirectory in home folder and chown it to my user
mkdir -p /home/luisubu/.ssh
chown luisubu:luisubu /home/luisubu/.ssh

# Create authorized_keys file, chmod and chown it
vi /home/luisubu/.ssh/authorized_keys
chmod 0400 /home/luisubu/.ssh/authorized_keys
chown luisubu /home/luisubu/.ssh/authorized_keys

# We need password-less access after authenticating via SSH keypair
# First, create a group
groupadd sysadmin

# Allow members of the sysadmin group password-less access
echo '%sysadmin ALL=(ALL) NOPASSWD:ALL' > /etc/sudoers.d/sysadmin

# Add my user to the sysadmin group
usermod -aG sysadmin luisubu

# Change default shell to bash (or something else if you prefer)
chsh -s /bin/bash luisubu

# Last, ansible depends on Python2 and it isn't present in the basic Ubuntu 16.04 image. Let's install it
sudo apt-get update
sudo apt-get install python

# more info
https://blog.simos.info/how-to-make-your-lxd-container-get-ip-addresses-from-your-lan/
https://blog.simos.info/how-to-make-your-lxd-containers-get-ip-addresses-from-your-lan-using-a-bridge/

Here is the iptables command. Set three parameters, and then change the $PORT to each port that needs to be opened.
`PORT=80 SERVER_IP=your_server_ip CONTAINER_IP=your_container_ip INTERFACE=your_server_network_interface sudo -E bash -c 'iptables -t nat -I PREROUTING -i $INTERFACE -p TCP -d $SERVER_IP --dport $PORT -j DNAT --to-destination $CONTAINER_IP:$PORT -m comment --comment "forward to network port"'`

Replace

PORT: the network port. In the example it shows port 80 (www).
SERVER_IP: the server’s IP address.
CONTAINER_IP: the container’s IP address (use lxc list to find it).
INTERFACE: the server network interface. Probably eth0 or something similar.

exemplos:
`PORT=8080 PROTO=tcp SERVER_IP=your_server_ip CONTAINER_IP=your_container_ip INTERFACE=your_server_network_interface sudo -E bash -c 'iptables -t nat -I PREROUTING -i $INTERFACE -p $PROTO -d $SERVER_IP --dport $PORT -j DNAT --to-destination $CONTAINER_IP:$PORT -m comment --comment "forward to Kodi network port 8080 TCP"' `

`PORT=9777 PROTO=udp SERVER_IP=your_server_ip CONTAINER_IP=your_container_ip INTERFACE=your_server_network_interface sudo -E bash -c 'iptables -t nat -I PREROUTING -i $INTERFACE -p $PROTO -d $SERVER_IP --dport $PORT -j DNAT --to-destination $CONTAINER_IP:$PORT -m comment --comment "forward to Kodi network port 8080 TCP"' `




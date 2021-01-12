# wg-proxy
proxy a wireguard connection with iptables. There will be 3 hosts: my laptop, server-01 and server-02 in vagrant. The host will make a wg connection to server-02 via server-01. note: the ip:s in the wg configs are hardcoded and need to be changed to run on other machines.

# test

````bash
# bring up wg interface on host
$ sudo wg-quick up ./wg/host/host.conf
# run vms
$ vagrant up
# add iptables rules on server-01
$ vagrant ssh server-01
$ cd /vagrant
$ iptables-save > wg/server-01/iptables.old
$ sudo ./wg/server-01/iptables.new
# bring up wg interface on server-02
$ vagrant ssh server-02
$ cd /vagrant
$ sudo wg-quick up ./wg/server-02/wg0.conf
````

run the test

````bash
# server-02
$ nc -l -s 10.200.100.10 -p 8989 -v
# host
$ nc 10.200.100.10 8989 -v
````

optionally validate ip addresses used with `lsof -anP -i:8989` on server-02

# license
MIT

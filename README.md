Configuração de rede no Ubuntu Server
Identificando interfaces Ethernet
Os nomes das interfaces comumente aparecem como eno1 ou enp0s25.
Comando: ip a

Saída:
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s25: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether 00:16:3e:e2:52:42 brd ff:ff:ff:ff:ff:ff link-netnsid 0
    inet 10.102.66.200/24 brd 10.102.66.255 scope global dynamic eth0
       valid_lft 3257sec preferred_lft 3257sec
    inet6 fe80::216:3eff:fee2:5242/64 scope link
       valid_lft forever preferred_lft forever

Configurando endereço de IP estático
1 - Copiando arquivo - realizando backup
sudo cp /etc/netplan/00-config.yaml /etc/netplan/00-config.yaml.bck
sudo vi /etc/netplan/00-static-config.yaml

Conteúdo:
network:
  version: 2
  renderer: networkd
  ethernets:
    eth0:
      addresses:
        - 10.10.10.2/24
      nameservers:
          search: [mydomain, otherdomain]
          addresses: [10.10.10.1, 1.1.1.1]
      routes:
        - to: default
          via: 10.10.10.1

Aplicando a configuração usando o comando: netplan

sudo netplan apply

referência

https://netplan.readthedocs.io/en/0.106/examples/#using-dhcp-and-static-addressing

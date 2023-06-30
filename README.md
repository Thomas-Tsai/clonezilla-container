# DRBL and Clonezilla Server

Docker file source for [DRBL](https://drbl.org) and [Clonezilla](https://clonezilla.org) container image.

## Basic

The DRBL and Clonezilla server need 2 network devices, one for internet access, another network device is intranet only. About the network configuration please check [doc](https://drbl.org/installation/). This image will use host network as DRBL and Clonezilla Server, please make sure you stop all realted service like: tftp, nfs, dhcp services.

to stop rpcbind(port 111) in debian like system:

```
sudo systemctl status rpcbind.socket 
```

and also remember to load nfs module before run drbl container

```
modprobe nfsd
```

## clonezilla

This image provide Clonezilla Server.

### run

```
docker run -itd --rm  --network=host --name=clonezilla --cap-add=ALL --privileged -e CLLAN=$DRBL-LAN-CARD -e CLLANIP=$DRBL-LAN-IP -v /home/partimag/:/home/partimag  tlinux/clonezilla:latest 

```

### logs

```
docker logs -f clonezilla
```

## drbl - diskless remote boot linux


This image provide DRBL and Clonezilla Server.

### run

```
docker run -itd --rm  --network=host --name=drbl --cap-add=ALL --privileged -e CLLAN=$DRBL-LAN-CARD -e CLLANIP=$DRBL-LAN-IP -v /home/partimag/:/home/partimag  tlinux/drbl:latest 
```

## logs

```
docker logs -f drbl
```

## more drbl/clonezilla usage

### dcs

```
docker exec -it drbl dcs
```

## Example

My Linux have 2 network interface, ens33 is for internet, ens38 is my LAN.

```
ens33: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.2.139  netmask 255.255.255.0  broadcast 192.168.2.255
        inet6 fe80::eee5:67da:390d:f5e1  prefixlen 64  scopeid 0x20<link>
        ether 00:0c:29:c1:94:96  txqueuelen 1000  (Ethernet)
        RX packets 8027034  bytes 10822801757 (10.8 GB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 1684725  bytes 1114428572 (1.1 GB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

ens38: flags=4419<UP,BROADCAST,RUNNING,PROMISC,MULTICAST>  mtu 1500
        inet 10.103.19.6  netmask 255.0.0.0  broadcast 10.255.255.255
        ether 00:0c:29:c1:94:a0  txqueuelen 1000  (Ethernet)
        RX packets 1679135  bytes 1765712576 (1.7 GB)
        RX errors 0  dropped 5  overruns 0  frame 0
        TX packets 846043  bytes 1222864098 (1.2 GB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

run clonezilla:

```
docker run -itd --rm  --network=host --name=clonezilla --cap-add=ALL --privileged -e CLLAN=ens38 -e CLLANIP=10.103.19.6 -v /home/partimag/:/home/partimag  tlinux/clonezilla:latest
```

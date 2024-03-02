### ubuntu as a autofs server & rocky linux as client

## 

```bash
apt update

```

## install autofs

```bash

apt install autofs

```

## ensure thate autofs service is active and enable 

```bash

systemctl status autofs 

```
## in /etc  \ip address is the client address

```bash

vim /etc/auto.nfs 
#nfs         -fstype=nfs   192.168.1.23:/var/share

```

## Edit auto.master file in /etc

```bash

vim /etc/auto.master

#/tmp        /etc/auto.nfs

```

## restart autofs service

```bash

systemctl restart autofs

``` 


# Nginx Basic Authentication configuration on docker 


## pull nginx docker image


```bash

yum update -y

docker pull nginx:1.25.3

```

## create docker volume

```bash

docker volume create nginx-etc

docker volume create nginx-html


```

## run nginx image mount two created volume to nginx config directory and html file directory



```bash


docker run -d --name nginx -v nginx-etc:/etc/nginx -v nginx-html:/usr/share/nginx/html -p 80:80 nginx:1.25.3

```

## install tools

```bash


yum install httpd-tools -y


```

## Create user & pass for authentication

```bash


htpasswd -c /var/lib/docker/volume/nginx-etc/_data/.htpasswd nginx 

# then enter pass for nginx user


```

## config file for basic authentication and redirectation 

```bash 

vim /var/lib/docker/volumes/nginx-etc/_data/conf.d/default.conf


```

#### add this two lines to server

![Alt text](<Screenshot 2024-01-22 134945.jpg>)


## reload nginx service 

```bash


docker exec -it nginx nginx:1.25.3 -s reload


```


![Alt text](<Screenshot 2024-01-23 120156.jpg>)






![Alt text](<Screenshot 2024-01-23 120613.jpg>)




![Alt text](<Screenshot 2024-01-23 120855.jpg>)







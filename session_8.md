create we and catalogue server with t2.mcro  and connect it through putty public ip addresses
give root access to instances using sudo su -
1. webapplication installation: here nginx used as webserver so install nginx in webserver
```````````````
 dnf install nginx -y
`````````````````
2. enable and start the nginx service

``````````
systemctl enable nginx
`````````````````

`````````````````
systemctl start nginx
````````````````````

3. access the service over browser

```````````````
public-ip:80
```````````````
4. remove the default content
 ``````````````````````````
 rm -rf /usr/share/nginx/html/*
 ````````
   

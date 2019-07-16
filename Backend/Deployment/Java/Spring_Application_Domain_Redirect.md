# Prerequisites 

1. Running application on any port except 80
2. nginx and apache web server

# Steps

This doc uses apache2 as an example

1. open apache2 configuration file.

```
sudo vi /etc/apache2/sites-available/000-default.conf
```

Note: `000-default.conf` this is default apache2 configuration file, name might change.

2. Add following block into configuration file

```
        ProxyRequests Off
        ProxyPreserveHost On
        ProxyPass / http://localhost:8080/
        ProxyPassReverse / http://localhost:8080/
```

Note: 8080 is the application running port, this might change depend on your application configuration.

3. restart web server

```
sudo service apache2 restart
```

Now, your application should be accessible on http://DOMAIN_NAME.com or http://INSTANCE_IP_ADDRESS:8080.com

# References

https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-18-04
https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/
https://medium.com/@codebyamir/using-apache-as-a-reverse-proxy-for-spring-boot-embedded-tomcat-f704da73e7c8
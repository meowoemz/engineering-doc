### Upload you application to ec2 directory

eg: `/var/www/myapp`


### Install as an `init.d` service

```
sudo ln -s /var/www/myapp/myapp.jar /etc/init.d/myapp
```

enable your app
```
sudo systemctl enable myapp
```

restart the service
```
sudo service myapp restart
```

### References
https://docs.spring.io/spring-boot/docs/current/reference/html/deployment-install.html
https://askubuntu.com/questions/921753/failed-to-start-mongod-service-unit-mongod-service-not-found
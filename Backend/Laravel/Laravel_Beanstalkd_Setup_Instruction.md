# Install Beanstalkd
```
sudo apt-get install beanstalkd
```

```
sudo vi /etc/default/beanstalkd 
```
change `BEANSTALKD_LISTEN_ADDR=127.0.0.1` to `BEANSTALKD_LISTEN_ADDR=0.0.0.0`

```
sudo service beanstalkd restart
```

use following tutorial
https://laravelista.com/posts/using-beanstalkd-with-laravel

# Add beanstalk console installation

# Configure Laravel

# Add Supervisor

use laravel official doc to create queue job

https://laravel.com/docs/5.4/queues

# References

http://www.kingpabel.com/beanstalkd-supervisor-laravel-queue/

https://laravelista.com/posts/using-beanstalkd-with-laravel

https://laravel.com/docs/5.4/queues

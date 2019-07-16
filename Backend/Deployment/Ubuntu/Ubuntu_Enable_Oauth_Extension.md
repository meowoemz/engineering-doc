### Install PEAR
```
sudo apt-get update
```
Depends on which version of PHP you're using, in this case we use **php5.6**
```
sudo apt-get install php-pear php5.6-dev
```
### Install Oauth Extension
From this point, you can use pear to install oauth extension
```
sudo apt-get install gcc make autoconf libc-dev pkg-config
```
```
sudo pecl install oauth-1.2.3
```
### Modify Environment Setting
You should add "extension=oauth.so" to php.ini

@ base directory
```
cd etc/php/5.6/cli/
```
```
sudo vi php.ini
```

Add following line into php.ini file
```
extension=oauth.so

```

Restart apache service including php
```
sudo service apache2 restart
```

Check mod already enabled
```
php -m
```


**References:**

http://codecreations.weebly.com/blog/installing-oauth-on-ubuntu

https://serverpilot.io/community/articles/how-to-install-the-php-oauth-extension.html

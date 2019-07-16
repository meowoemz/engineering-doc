### Prerequisites
Directories contain different projects files
```
/var/www/example1
/var/www/example2
```
```
sudo chmod -R 755 /var/www
```

### Step One — Create New Virtual Host Files

```
sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/example1.conf
```
Open the new file in your favourite editor with root privilege:
```
sudo vi /etc/apache2/sites-available/example1.com.conf
```
It should be something like this: 
```
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
Modify it to following format
```
<VirtualHost exmaple1.com:80>
    ServerName example1.com
    ServerAlias www.example1.com
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/exmaple1
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
If you have two sites launch on server, you should have two similar files with this format.
```
example1.conf
example2.conf
```

### Step Two — Enable the New Virtual Host Files
```
sudo a2ensite example1.conf
sudo a2ensite example2.conf
```
Restart your apache service, both of these commands could work, pick one
```
sudo systemctl restart apache2
sudo service apache2 restart
```

### Step Three - Set Up Local Hosts File (Optional)
```
sudo vi /etc/hosts
```
Assuming VPS IP address is xxx.xxx.xxx.xxx
```
127.0.0.1   localhost
127.0.1.1   guest-desktop
xxx.xxx.xxx.xxx example1.com
xxx.xxx.xxx.xxx example2.com
```


References:

https://www.digitalocean.com/community/tutorials/how-to-set-up-apache-virtual-hosts-on-ubuntu-16-04

nginx: https://www.digitalocean.com/community/tutorials/how-to-set-up-nginx-server-blocks-virtual-hosts-on-ubuntu-16-04
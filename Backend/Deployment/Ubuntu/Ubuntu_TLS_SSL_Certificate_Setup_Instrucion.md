### Prerequisites

**1.** An Ubuntu 16.04 server with a non-root sudo user

**2.** The Apache web server installed with one or more domain names properly configured through Virtual Hosts that specify ```ServerName```

### Step 1 — Install the Let's Encrypt Client
```
sudo apt-get update
sudo apt-get install python-letsencrypt-apache
```

### Step 2 — Set Up the SSL Certificate

```
sudo letsencrypt --apache -d example.com
```
you want to install a single certificate that is valid for multiple domains or subdomains
```
sudo letsencrypt --apache -d example.com -d www.example.com
```

### Step 3 — Set Up Auto Renewal
this command would renew the certificate
```
sudo letsencrypt renew
```

Setup a cron job
```
sudo crontab -e
```
Select your favourite editor
Include following content at the end of the crontab
```
30 2 * * 1 /usr/bin/letsencrypt renew >> /var/log/le-renew.log
```

References:

https://www.digitalocean.com/community/tutorials/how-to-secure-apache-with-let-s-encrypt-on-ubuntu-16-04

http://www.wpbeginner.com/wp-tutorials/how-to-add-free-ssl-in-wordpress-with-lets-encrypt/

This instruction is for ```ubuntu 16.04```, if you have different version server, commands might have slight differences.
For ```ubuntu 14.04```, read following tutorial

https://www.digitalocean.com/community/tutorials/how-to-secure-apache-with-let-s-encrypt-on-ubuntu-14-04
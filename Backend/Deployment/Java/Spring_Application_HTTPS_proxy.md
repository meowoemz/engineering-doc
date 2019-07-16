If you already setup domain redirect, follow the steps, if not, go through 


1. install letsencrypt cert-bot

```
$ sudo apt-get update
$ sudo apt-get install software-properties-common
$ sudo add-apt-repository ppa:certbot/certbot
$ sudo apt-get update
$ sudo apt-get install python-certbot-apache
```

2. Automate certificate installation
```
$ sudo certbot --apache
```

If apache2 configuration is setup correctly, everything should be working.
If not, you can create certification separately, stop your web server first.
```
$ sudo certbot --apache certonly
```

# References
https://certbot.eff.org/lets-encrypt/ubuntubionic-apache
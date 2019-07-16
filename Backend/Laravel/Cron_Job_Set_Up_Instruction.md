# Cron job

checkout to root user

`sudo -i`

open crontab to edit

`crontab -e`

then you could see something like this, follow the crontab format to setup customize command

https://www.pantz.org/software/cron/croninfo.html

```
# For example, you can run a backup of all your user accounts
# at 5 a.m every week with:
# 0 5 * * 1 tar -zcf /var/backups/home.tgz /home/

*/5 * * * *     root    tmpreaper -a 5m /tmp/
```
# Prerequisites

1. Previous site WordPress admin login information.

2. Server login information.

3. Database connection information(optional).

4. System requirement: `Ubuntu 16.10/16.04`

# Site Migration
## Step one: copy theme and plugins

1. login to server which host old site via `ssh` using terminal.
```
ssh USER_NAME@SERVER_IP_ADDRESS
```

2. locate theme and plugin directories, usually these files are located at `wp-content`.

3. create `git` repositories store these files.

helpful git commands:
```
git init
git add .
git commit -m "SOME MESSAGES"
git push origin SOME_ORIGIN
```
## Step two: create new WordPress host for site
1. Login to server you wish to host the WordPress site just you did in the first step.

2. Install WordPress CMS.

locate a directory you wish to install WordPress
```
wget -c http://wordpress.org/latest.tar.gz
tar -xzvf latest.tar.gz
```
you need to move all WordPress files one directory up 
```
sudo mv * ../
```

change default directory owner and permission
```
sudo chown -R www-data:www-data /var/www/YOUR_DIR/
sudo chmod -R 755 /var/www/YOUR_DIR/
```

if you don't use `html` as your default directory, you need to setup multiple host on your server, detail
steps see 
https://github.com/moregold/engineering-doc/blob/master/Backend/Apache2_Multiple_Virtual_Hosts_Setup_Instruction.md
## Step three: export WordPress site file from admin page
1. go to site address, add `/admin` after base URL.

2. prompt username and password.

3. At left side bar, select **`Tools`**->**`Export`**, leave it as default configuration, 
which is **`All content`**, click **`Download Export File`**.

## Step four: import WordPress file to new server
1. Enter URL to visit new web server.

2. config your WordPress Database, WordPress would create a MySQL database as default,
if you have a database setup elsewhere, you should create a `wp-config.php` file in you server directory,
put your database credential in this file.
```
Database name
Database username
Database password
Database host
```

3. Create admin user for new WordPress site, after submit, your UI should be exactly same as the old admin WordPress page.

4. **(Important)** clone `theme` and `plugins` repositories you copied in step one, you can locate `theme` and `plugins` directories
in `wp-content`, active plugins, keep the configurations the same as old site.

5. At left side bar, **`Tools`**->**`Import`**, install WordPress importer, you should keep your directory owner as `www-data`, otherwise WordPress
would keep asking you the server FTP credentials.

6. Full import supposed to keep the same configurations, but you should double check your old site and the new one.
make sure all settings are identical.

References:

http://www.tecmint.com/install-wordpress-on-ubuntu-16-04-with-lamp/

https://codex.wordpress.org/Creating_a_Static_Front_Page

https://managewp.com/wordpress-migrating-content-and-media

https://www.digitalocean.com/community/tutorials/how-to-install-wordpress-with-lemp-on-ubuntu-16-04

https://www.digitalocean.com/community/tutorials/how-to-install-linux-nginx-mysql-php-lemp-stack-in-ubuntu-16-04


## Another way to accomplish this

Delete all files end in with `.php` extension in current directory and sub directory.

`find . -type f -iname '*.php' -exec rm {} \;`

`find . -name "*.php" -exec rm -f {} \;`

ssh copy all files located in `wp-content` to local, and upload them to new server.

> remote to local

`scp -r user@your.server.example.com:/path/to/foo /tmp/`

> local to remote

`scp -r  /tmp/foo user@your.server.example.com:/path/to/foo`


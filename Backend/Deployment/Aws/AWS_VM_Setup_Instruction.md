# Virtual Machine Setup
## Step 1: Choose AMI(Amazon Machine Image)
Select specific server type, we chose **Ubuntu Server 16.04 LTS (HVM), SSD Volume Type** for instance.

## Step 2: Choose an Instance Type
Choose combinations of CPU, memory, storage, and networking capacity, they can fit different use cases. **t2.micro** for 
instance.

## Step 3: Configure Instance Details
Configure the instance to suit your requirements. You can launch multiple instances from the same AMI, request Spot 
instances to take advantage of the lower pricing, assign an access management role to the instance, and more. Remain **default** in 
this case.

## Step 4: Add Storage
You can attach additional EBS volumes and instance store volumes to your instance, or edit the settings of the root volume. 
You can also attach additional EBS volumes after launching an instance, but not instance store volumes. Remain **default** in 
this case.

## Step 5: Tag Instance
a tag contains a **case-sensitive** key-value pair.
see following URL to learn more: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Using_Tags.html?icmpid=docs_ec2_console

## Step 6: Configure Security Group
two options: create a new one, select an existing security group

we use SSH(for linux) port 22, HTTP port 80 and HTTPS port 443 for basic protocol

**Add Rule**->select desire protocol->remain default config


## Review and Launch
after click launch, AWS would deploy your server instance, and the status should be **running**.


# Connect to Virtual Machine(VM)
download private key file (should be in SERVER_NAME.pem).

move it into ssh directory:
```
mv SERVER_NAME.pem ~/.ssh/
```

set the key file into private if needed:
```
chmod 400 SERVER_NAME.pem
```

go to the directory where stored your key file:
```
cd ~/.ssh/
```

connect to your server instance using its **Public DNS**, you can find it in **Description**, in this case: 

ec2-54-244-205-206.us-west-2.compute.amazonaws.com

```
ssh -i "Dev_zcn.pem" ubuntu@ec2-54-244-205-206.us-west-2.compute.amazonaws.com
```

your terminal should prompt something like this:
```
ubuntu@ip-XXX-XX-XX-XXX:
```
It means you already connected to your VM on AMS, congrats!

**Important!**

On a Linux instance, the public key content is placed in an entry within ~/.ssh/authorized_keys. This is done at boot time and enables you to securely access your instance without passwords. 

If you accidentally changed your authorized_keys file on your virtual machine, you can't login as ```ubuntu``` user, here's the way to restore your key file.

At your local machine
```
ssh-keygen -y
```

When prompted to enter the file in which the key is, specify the path to your .pem file; for example:
```
/path_to_key_pair/my-key-pair.pem
```

The command returns the public key:
```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQClKsfkNkuSevGj3eYhCe53pcjqP3maAhDFcvBS7O6V
hz2ItxCih+PnDSUaw+WNQn/mZphTk/a/gU8jEzoOWbkM4yxyb/wB96xbiFveSFJuOp/d6RJhJOI0iBXr
lsLnBItntckiJ7FbtxJMXLvvwJryDUilBMTjYtwB+QhYXUMOzce5Pjz5/i8SeJtjnV3iAoG/cQk+0FzZ
qaeJAAHco+CY/5WrUBkrHmFJr6HcXkvJdWPkYQS3xqC0+FmUZofz221CBt5IMucxXPkX4rWi+z7wB3Rb
BQoQzd8v7yeb7OzlPnWOyN0qFU0XA246RA8QFYiCNYwI3f05p6KLxEXAMPLE
```
you can login your virtual machine as other users(if there's no other user, you should re-install your VM)
switch to ```root``` user
```
sudo -i
```

switch to ```ubuntu``` user
```
su ubuntu
```

go to ```.ssh``` folder, edit your key file with editor
```
cd ~/.ssh/
```
```
sudo vi authorized_keys
```

just copy and paste this content into the ```authorized_keys``` file, then you can restore your login 

# install apache2/nginx on VM
**Caution: following commands are executed on your VM shell**
```
sudo apt-get update
```
```
sudo apt-get install apache2 mysql-server
```

For nginx
```
sudo apt-get install nginx
```

## install php
```
sudo add-apt-repository ppa:ondrej/php
```
```
sudo apt update
```
```
sudo apt install php5.6 libapache2-mod-php5.6 php5.6-curl php5.6-gd php5.6-mbstring php5.6-mcrypt php5.6-mysql php5.6-xml php5.6-xmlrpc
```
```
sudo a2enmod php5.6
```
```
sudo systemctl restart apache2
```
```
sudo service apache2 restart
```


# Test Apache2(Deploy Test Web Project On VM)
At this step, you can access Apache2 default index page using **Public DNS** we mentioned above, 
if you want to deploy your own web project, you need to clone you project folder into index directory.
Make sure you are under VM root directory: 
```
bin   etc         lib         media  proc  sbin  sys  var
boot  home        lib64       mnt    root  snap  tmp  vmlinuz
dev   initrd.img  lost+found  opt    run   srv   usr
ubuntu@ip-172-31-17-178:/$ 
```
**1. change the directory permission:**
```
sudo chmod 777 var
```
**2. go to index directory:**
```
cd var/www/html/
```

**3. delete original index page:**
```
rm index.html
```

## Deploy Web Project on your VM
**ignore this part if you already know how to clone project into a folder**
**And clone your web project into current directory folder /var/www/html**

**1. Generate a ssh key:**
```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

**2. Open id_rsa.pub file, copy the public key**
```
cd ~/.ssh/
```
```
vi id_rsa.pub
```

Log into your GitHub account
**Settings->SSH and GPG keys->New SSH key**
Add description and paste the key you copy from id_rsa.pub

See details in: https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/

**Setting up Git**
```
git config --global user.name "YOUR NAME"
```
```
git config --global user.email "YOUR EMAIL ADDRESS"
```
see details in: https://help.github.com/articles/set-up-git/

**3. Return to index directory**

**4. Clone your web directory into index directory**
```
git clone YOUR_PROJECT_URL .
```
### Now you can access your web application using Public DNS

## Config Apache2 header rewrite
**1. Add following block into two files**

```
sudo vi etc/apache2/sites-available/000-default.conf
```
```
<Directory /var/www/html>
    Options Indexes FollowSymLinks MultiViews
    AllowOverride All
    Order allow,deny
    allow from all
</Directory>
```

var/www/html, create .htaccess file
```
cd var/www/html
```
```
sudo vi .htaccess
```

```
RewriteEngine On
RewriteRule ^ - [E=HTTP_AUTHORIZATION:%{HTTP:Authorization}]

RewriteCond %{REQUEST_FILENAME} !-d
RewriteCond %{REQUEST_FILENAME} !-f
RewriteRule ^ public/index.php [L]
```

**2. Enable Apache2 mod-rewrite**
```
sudo a2enmod rewrite
```

```
sudo service apache2 restart
```
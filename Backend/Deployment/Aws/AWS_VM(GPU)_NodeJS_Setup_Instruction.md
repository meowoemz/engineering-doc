# Setup VM

use the documentation AWS_VM_Setup_Instruction

# Install Node.js

```
sudo apt-get update
```
```
sudo apt-get install nodejs
```
```
sudo apt-get install npm
```

there're three ways to install Node.js, choose your preferred one, in this documentation, we choose the first one.

as default, following command would help you to ues `node` and `nodejs` at the same time.
```
sudo ln -s /usr/bin/nodejs /usr/local/bin/node
```

# Setup a Node server

use following link to setup one easy node server

https://medium.freecodecamp.com/building-a-simple-node-js-api-in-under-30-minutes-a07ea9e390d2

after setup, you could use `POSTMAN` to test your server

under project root directory, run
```
node server.js
```
it should start the server

# Setup server as one service

There're several ways to do this, in this documentation, we use one plugin call `PM2`.

official website: http://pm2.keymetrics.io/

`npm install pm2 -g`, you may need to run this command as `sudo`

at this point, instead using `node server.js`, you could run to start your serve
```
pm2 start server.js
```
add your serve as startup service to ubuntu
```
pm2 startup
```
Example
```
[PM2] You have to run this command as root. Execute the following command:
      sudo su -c "env PATH=$PATH:/home/unitech/.nvm/versions/node/v4.3/bin pm2 startup <distribution> -u <user> --hp <home-path>
```

# References

https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-16-04

https://medium.freecodecamp.com/building-a-simple-node-js-api-in-under-30-minutes-a07ea9e390d2

AWS Pricing http://www.ec2instances.info/?selected=cr1.8xlarge

AWS Instance introduction https://aws.amazon.com/ec2/instance-types/

https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/System_Administrators_Guide/sect-Managing_Services_with_systemd-Unit_Files.html

http://pm2.keymetrics.io/docs/usage/startup/
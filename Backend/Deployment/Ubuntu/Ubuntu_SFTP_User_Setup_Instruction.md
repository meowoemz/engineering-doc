# Prerequisites

One Ubuntu 16.04 server set up with this initial server setup tutorial, including a sudo non-root user and a firewall.

log in as root user

## Creating a New User

```
adduser USER_NAME
```
configure user, make sure user could connect to serve with ssh, see details


## Connect to FTP server

we use `FileZilla` in this case.

Create new connection

- enter Host
- SFTP SSH File Transfer Protocol
- Logon Type as Key file
- User as username on server
- Key file as private key file in your local machine

### References

https://www.digitalocean.com/community/tutorials/how-to-enable-sftp-without-shell-access-on-ubuntu-16-04
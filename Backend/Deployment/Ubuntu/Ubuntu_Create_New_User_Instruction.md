**All following operations are based on Ubuntu 16.04**

**Login as root**
```
adduser NEW_USER
```
Choose your password, (optional)Enter personal information.

**Add User into _sudo_ Group**
```
usermod -aG sudo NEW_USER
```

**Generate Key Pairs**

If you already have public and private key pairs, skip this part, @local machine.
```
ssh-keygen
```
Leave the default storage location, should be **~/.ssh/**, you can enter password or (recommended) leave it blank.

**Copy the public key**

Go to **~/.ssh/**
```
cd ~/.ssh/
```

_Option - 1_
```
cat ~/.ssh/id_rsa.pub
```

_Option - 2_
```
vi ~/.ssh/id_rsa.pub
```

key pattern should be like following format: 
```
ssh-rsa AAAAB3NzaC1ycXEAAAADAQABAAABAQC4NXYHaXQDLUJDMLhCQYluDVo2HQbdIO/mEkmbI/ucNtxcuIrsFd5FQvHKmHjJ5Ep/7sI+NWmDbY7pAWOu2pK8/
xF+4l34ueP+XYwQMUgBwYYXaSjtkMjuSH0stRXJbRpYjmB+ncKvvUSll6ElmYvfsUTFOyHW4kUPAvkm0CQ4jtVIUZQydnbPxBsi6Q5UHJdPqJhco794zYyqXKw29x
a6H7QxBR0DzeYCf1+3N5cRcFAOaG/+s87wyjVezqbCkqdWWkuM6KFXOdL06PfEnNTRh4FrymzlE/qRTrTB8Zk3t01wgym4bJ06eetTgYOx660Xc7TBHKIyQeIz/JmGGLMf

```
Copy the key.

**Add Key into server**

Change to user just created
```
su - NEW_USER
```

Create a new .ssh folder and change its permission
```
mkdir ~/.ssh
```
```
chmod 700 ~/.ssh
```

Create a ```authorized_keys``` file
```
vi ~/.ssh/authorized_keys
```
Copy the key into new file

Change file access mod
```
chmod 600 ~/.ssh/authorized_keys
```
```
exit
```
##Now you can access remote server on your machine
```
ssh NEW_USER@SERVER_IP_OR_PUBLIC_DNS
```

**References**
https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-16-04
# Prerequisite

1. Ec2 instance
2. S3 bucket
3. aws access-key and access-secret

# Setup Process

1. Login to your ec2 instance

update system
```
sudo apt-get update
```

2. Install dependencies
```
sudo apt-get install automake autotools-dev fuse g++ git libcurl4-gnutls-dev libfuse-dev libssl-dev libxml2-dev make pkg-config
```

3. Clone s3fs
```
git clone https://github.com/s3fs-fuse/s3fs-fuse.git
```

4. install
```
cd s3fs-fuse
./autogen.sh
./configure --prefix=/usr --with-openssl
make
sudo make install
```

5. Setup aws credential
```
sudo vi /etc/passwd-s3fs
```
```
Your_accesskey:Your_secretkey
```

6. Change file permission
```
sudo chmod 640 /etc/passwd-s3fs
```

7. Mount S3
```
sudo mkdir /mys3bucket
```

```
sudo s3fs your_bucketname -o use_cache=/tmp -o allow_other -o uid=1001 -o mp_umask=002 -o multireq_max=5 /mys3bucket
```

where, “your_bucketname” = the name of your S3 bucket that you have created on AWS S3,
use_cache = to use a directory for its cache purpose,
allow_other= to allow other users to write to the mount-point,
uid= uid of the user/owner of the mountpoint (can also add “-o gid=1001” for group),
mp_umask= to remove other users permission. multireq_max= parameter to send request to s3 bucket,
/mys3bucket= mountpoint where the bucket will be mounted.

```
sudo umount /mys3bucket
```

8. Test
```
cd /mys3bucket
echo "this is a test file to check s3fs" >> test.txt
ls
```

References:

https://cloudkul.com/blog/mounting-s3-bucket-linux-ec2-instance/

https://kb.iu.edu/d/adwf
Append following block into your nginx.conf file which in `/etc/nginx`:

Add it to site block
```
server{
    add it here
}
```
```
location ~ ^/(wp-admin|wp-login\.php) {
                allow 1.2.3.4;
                deny all;
  }
```

you can add multiple ip addresses, but stay the same sequence, `allow` first, `deny` must be the last line of the block.


If your serve is apache, the syntax might be slight different, and you need to 
locate apache2 config file as well.

**_References:_**

https://www.cyberciti.biz/faq/nginx-block-url-access-all-except-one-ip-address/

https://codex.wordpress.org/Brute_Force_Attacks
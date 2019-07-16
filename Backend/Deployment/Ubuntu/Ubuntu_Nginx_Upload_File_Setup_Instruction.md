# Modify Nginx Upload File Max Size

add following line into nginx.conf `http` or `serve` or `location`, one of the locations is fine.

```
client_max_body_size 10M;
```

You should also modify `php.int`

```
upload_max_filesize = 10M
post_max_size = 10M
```

restart nginx serve, and reload php-fpm/php service.
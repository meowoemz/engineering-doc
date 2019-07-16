# Setup AWS_S3 CORS(Cross-Origin Resource Sharing)

Go to your S3 bucket, at `Permissions` tab, Click `CORS configuration` tab.

```
<?xml version="1.0" encoding="UTF-8"?>
<CORSConfiguration xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
<CORSRule>
    <AllowedOrigin>http://example.com</AllowedOrigin>
    <AllowedMethod>HEAD</AllowedMethod>
    <AllowedMethod>GET</AllowedMethod>
    <AllowedMethod>PUT</AllowedMethod>
    <AllowedMethod>POST</AllowedMethod>
    <AllowedMethod>DELETE</AllowedMethod>
    <MaxAgeSeconds>1</MaxAgeSeconds>
    <ExposeHeader>Server</ExposeHeader>
    <AllowedHeader>Authorization</AllowedHeader>
</CORSRule>
</CORSConfiguration>
```

copy above code into code area and save, test your web.
 
# References

http://docs.aws.amazon.com/AmazonS3/latest/API/RESTCommonRequestHeaders.html

http://docs.aws.amazon.com/AmazonS3/latest/API/RESTCommonResponseHeaders.html

http://docs.aws.amazon.com/AmazonS3/latest/dev/cors.html

http://docs.aws.amazon.com/AmazonS3/latest/dev/cors.html#how-do-i-enable-cors

https://www.html5rocks.com/en/tutorials/cors/


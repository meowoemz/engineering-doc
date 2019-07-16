# Prerequisite
`AWS Access Key Id` 

`AWS Access Key Secret`

`Aws\S3\S3Client`: include "aws/aws-sdk-php": "2.*" in your `composer.json` if you use `laravel` framework

# Upload
## Direct Upload
1. Login into your AWS account, at **`Services`**/**`Storage`** section, select **`S3`**

2. If you already create a bucket, click into your bucket, you can also create folder in your bucket,
 you can upload files by clicking `Upload` button
 
 
## Script Upload

**1. Create s3 object**
```
$s3 = S3Client::factory(array(
            'credentials' => array(
                'key' => 'AWS Access Key Id',
                'secret' => 'AWS Access Key Secret'
            )
        ));
```


**2. Upload local file or object to S3**
```
$result = $s3->putObject(array(
            'Bucket' => 'YOUR_BUCKET_NAME',
            'Key' => 'FILE_NAME',
            'Body' => fopen('PATH_TO_LOCAL_FILE', 'r+'),
            'ACL' => 'public-read'
        ));
```

## References:

http://docs.aws.amazon.com/aws-sdk-php/v2/guide/service-s3.html

http://docs.aws.amazon.com/AmazonS3/latest/dev/UploadObjSingleOpPHP.html

http://docs.aws.amazon.com/aws-sdk-php/v2/api/class-Aws.S3.S3Client.html#_putObject

### **_Download File Via URL_**
http://stackoverflow.com/questions/6348602/download-remote-file-to-server-with-php

### **_Get S3 Object URL_**
http://stackoverflow.com/questions/18459035/aws-s3-php-api-how-to-get-url-after-file-upload


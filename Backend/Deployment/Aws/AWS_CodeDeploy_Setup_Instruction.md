### To perform code autoDeploy on AWS, Check following prerequisites:
 
 **An IAM role must be attached to your instance**
 
 **Your AWS EC2 instance must be tagged**
 Eg:
  
    Key(name) - Value(your_instance_name)
 
 **The AWS CodeDeploy agent must be installed and running on the Amazon EC2 instance**
 
 For the first two steps, follow the instructions of AWS documentation which link below
 
 http://docs.aws.amazon.com/codedeploy/latest/userguide/how-to-configure-existing-instance.html
 
 We emphasize how to install ```AWS CodeDeploy agent``` on your VM. In our case, we use ```Ubuntu 16.04``` and 
 ```Apache2```, if you have different EC2 instance, instructions might change.
 
 Make sure you running following code at first time you sign in to your EC2 instance (```Ubuntu 16.04```)
 
 ```
 sudo apt-get update
 ```
 ```
 sudo apt-get install python-pip
 ``` 
 ```
 sudo apt-get install software-properties-common
 ``` 
 ```
 sudo apt-add-repository ppa:brightbox/ruby-ng
 ```
 ```
 sudo apt-get update
 ```
 ```
 sudo apt-get install ruby2.0
 ```
 ```
 sudo apt-get install wget
 ```
 ```
 cd /home/ubuntu
 ```
 ```
 wget https://bucket-name.s3.amazonaws.com/latest/install
 ```
 Replace ```bucket-name```:
 
 ```aws-codedeploy-us-east-1``` for instances in the US East (N. Virginia) region
 
 ```aws-codedeploy-us-east-2``` for instances in the US East (Ohio) region
 
 ```aws-codedeploy-us-west-1``` for instances in the US West (N. California) region
 
 ```aws-codedeploy-us-west-2``` for instances in the US West (Oregon) region
 
 ```aws-codedeploy-ap-south-1``` for instances in the Asia Pacific (Mumbai) region
 
 ```aws-codedeploy-ap-northeast-2``` for instances in the Asia Pacific (Seoul) region
 
 ```aws-codedeploy-ap-southeast-1``` for instances in the Asia Pacific (Singapore) region
 
 ```aws-codedeploy-ap-southeast-2``` for instances in the Asia Pacific (Sydney) region
 
 ```aws-codedeploy-ap-northeast-1``` for instances in the Asia Pacific (Tokyo) region
 
 ```aws-codedeploy-eu-central-1``` for instances in the EU (Frankfurt) region
 
 ```aws-codedeploy-eu-west-1``` for instances in the EU (Ireland) region
 
 ```aws-codedeploy-sa-east-1``` for instances in the South America (São Paulo) region
 
 ```
 chmod +x ./install
 ```
 ```
 sudo ./install auto
 ```
 ```
 sudo service codedeploy-agent start
 ```
 ```
 sudo service codedeploy-agent status
 ```
 For some reason, ```Ubuntu 16.04``` would install the newest version of ```ruby``` which is 2.3, 
 but for code deploy we need old version of ```ruby``` 2.0.
 
 https://www.brightbox.com/docs/ruby/ubuntu/
 
 If you want to install AWS CodeDeploy agent on different OS, check the following link
 
 http://docs.aws.amazon.com/codedeploy/latest/userguide/how-to-run-agent-install.html
 
 
 **Login to your AWS CodeDeploy console**
 
 
1. ```Create New Application``` on the left upper corner
    
    Specify ```Application Name``` and ```Deployment Group Name```.
    
    Choose your instance, use Key - Value to find EC2 instance, normally ```Name``` is the first option.
    
    If you have multiple instances to deploy, choose corresponding ```Deployment Config```.
    
    Leave ```Triggers``` and ```Alarms``` part as default except you have specific need.
    
    Better check ```Roll back when a deployment fails``` box.
    
    Select the correct role for ```Service Role ARN```

2. Click into the application you just created, ```Create deployment group```

    Specify a ```Deployment Group Name```

    AWS CodeDeploy requires the following for each instance that it deploys to:
        
        1. Each Amazon EC2 instance must launch with the correct IAM instance profile attached. 
        
        2. Each Amazon EC2 instance must have identifying Amazon EC2 tags or be in an Auto Scaling group.
        
        3. Each on-premises instance must have an associated IAM user, identifying on-premises instance tags, and a special configuration file.
        
        4. The AWS CodeDeploy agent must be installed and running on each instance.
 
 **At this point, you have all prerequisites for AWS CodeDeploy**
 
 each instance must contain an ```appsec.yml``` file at root directory of you application, format could be like this: 
 
 ```
 version: 0.0
 os: linux
 files:
    - source: /
      destination: /var/www/html
 permissions:
    - object: /var/www/html
      pattern: "**"
      owner: apache
      group: apache
      mode: 755
      type:
        - file
 hooks:
    BeforeInstall:
     - location: scripts/installapache.sh
       runas: root
     - location: scripts/startapache.sh
       runas: root
    AfterInstall:
     - location: scripts/restartapache.sh
       runas: root
 ```
 
 In addition, depends on your system configuration, ```hooks``` might be change.
 According to the ```hooks```, add following files into your application ```scripts``` folder at root directory.
 
 **installapache.sh**
 ```
 #!/bin/bash
 apt-get install apache > /var/log/installapache.out 2>&1
 ```
 
 **startapache.sh**
 ```
 #!/bin/bash
 service apache2 start > /var/log/startapache.out 2>&1
 ```
 
 **restartapache.sh**
 ```
 #!/bin/bash
 service apache2 restart > /var/log/restartapache.out 2>&1
 ```
 
 **Important!! This is the last step**
 
 use following link to configure your Github account in order to connect to AWS CodeDeploy
 
 https://aws.amazon.com/blogs/devops/automatically-deploy-from-github-using-aws-codedeploy/
 
 
 **References**: 
 
 https://github.com/andrewpuch/code_deploy_example
 
 https://plus.google.com/105421247597792372605/posts/aH4KPw7YnyK
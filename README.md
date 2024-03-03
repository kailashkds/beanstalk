# Beanstalk
There are following steps for adding ssl to beanstack.

***1) Nginx Configuration***

We need to have a url that return 200 status code so that beanstack can do health check. Below is the path where you the nginx file should be in the root of your folder.

`.platform/nginx/conf.d/elasticbeanstalk/nginx.conf`
you need to add below code in your nginx file just above `location / {`

````
location /health {
    access_log off;
    add_header 'Content-Type' 'application/json';
    return 200 '{"status": "UP"}';
}
````

***2) Create SSL certificate***

https://ap-south-1.console.aws.amazon.com/acm/home?region=ap-south-1#/certificates/request

**Note: your ssl certicate should be on the same zone as your beanstack**

***3) Configure load balancer on your beanstack***

***4) Route your 443 request to 80 over Beanstack***

***5) Zip your folder and upload***
Create a zip file using below code. 
``zip ../symfony-default.zip -r * .[^.]* -x "vendor/*"``

Here {{ symfony-default.zip }} can be your zip file name

**Note: you need to execute the above code from root of your foler not outside the root folder**


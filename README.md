# set UP VPC 
![vpc-form-filled](https://github.com/RaihanIIUC/forntend-deploy-using-vpc-with-load-balancer/assets/51045712/fc798f92-6fac-461e-bc6d-2b7bd84d5e4f)


# set up NAT 
![nat-form-filled](https://github.com/RaihanIIUC/forntend-deploy-using-vpc-with-load-balancer/assets/51045712/e6289aa9-d431-4016-ae7e-88163431c84f)

#### create route inside NAT
![nat-router--form](https://github.com/RaihanIIUC/forntend-deploy-using-vpc-with-load-balancer/assets/51045712/a80d4376-94fe-4157-905e-78d28e6c04b9)


# create VM form private IP template instance 

![vm-private-ip-template-filled](https://github.com/RaihanIIUC/forntend-deploy-using-vpc-with-load-balancer/assets/51045712/12b0fe80-3d7f-4669-bd9c-38586f9c8ee2)



# Load Balance Setup 

![vpc-public-ip-template](https://github.com/RaihanIIUC/backend-deploy-in-vpc-with-load-balance/assets/51045712/f3a6439d-b06d-475b-b0a9-d15654e53a54)

we create a public ip available vm instance template so that we can make a load balance cloing the publically setted template.

## Inside LoadBalance

`cd /etc/nginx`
`ls`
`sudo nano nginx.conf` change this conf file as needed :


`events {
    # empty placeholder
}


http {

    server {
        listen 80;

        location / {
            proxy_pass http://frontend-raihan;
        }

        location /api/ {
            rewrite ^/api/(.*)$ /$1 break;
            proxy_pass http://backend-raihan;
        }
    }

    upstream frontend-raihan {
        server 11.10.10.12:80;
        server 13.10.10.14:80;
    }

    upstream backend-raihan {
        server 10.10.0.5:8000;
        server 11.10.10.6:8080;
    }
}`

`location /api/ {
            rewrite ^/api/(.*)$ /$1 break;
             proxy_pass http://backend-raihan;
}`

`upstream backend-raihan {
       server 10.10.0.5:8000;
       server 11.10.10.6:8080;
}` set two backend there so that whenever you have huge request it will auto transfer user to other one.


# set up frontend 

* `https://github.com/nodesource/distributions` take v-16 binary version
* sudo corepack enable to enable yarn
* clone this to there
* `yarn`
* `npm install`
* `npm run dev`


# Backend port setup 
 * open BaseUrl.js  file and change the port for backend.

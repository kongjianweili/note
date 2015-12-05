1  server {
 2   listen 8888;
 3   resolver 8.8.8.8;
 4   location /{
 5   #   proxy_pass http://$http_host$request_uri;
 6     proxy_pass $scheme://$host$request_uri;
 7     proxy_set_header X-Real-IP $remote_addr;
 8     proxy_set_header Host $host;
 9     proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
10
11     proxy_http_version 1.1;
12     proxy_set_header Upgrade $http_upgrade;
13     proxy_set_header Connection "upgrade";
14
15     client_max_body_size 100m;
16
17     #allow 127.0.0.1;
18     #deny all;
19   }
20   access_log   /var/log/nginx/proxy-access.log;
21   error_log    /var/log/nginx/proxy-error.log;
22 }

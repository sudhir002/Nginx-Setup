# Nginx-Setup
Nginx Setup on EC2, Ubuntu, Linux





login to server


1.sudo apt update


2.sudo api install nginx -y


3.sudo nano /etc/nginx/nginx.conf


        // make related lines like this

        include /etc/nginx/conf.d/*.conf;
        #include /etc/nginx/sites-enabled/*;
        include /etc/nginx/sites-available/*;


4.sudo nano /etc/nginx/sites-available/default


remove everything and paste


server {


  listen 80;


  server_name 127.0.0.1 localhost;


  client_max_body_size 50M;


  location /sc1/ {
  
  
    add_header 'Access-Control-Allow-Origin' '*' always;
    
    
    add_header 'Access-Control-Allow-Credentials' 'true';
    
    
    add_header 'Access-Control-Allow-Methods' 'GET, POST, PATCH, PUT, DELETE, OPTIONS';
    
    
    add_header 'Access-Control-Allow-Headers' 'Authorization,DNT,X-CustomHeader,Keep-Alive,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type';
    
    
    rewrite ^/sc1/(.*) /$1 break;
    
    
    proxy_pass http://127.0.0.1:8000;
    
    
  }
  
  

}


5.sudo systemctl restart nginx


6.enable port in security grp of server


               it will be like this (source anywere 0.0.0.0/0 for port 80 and others)




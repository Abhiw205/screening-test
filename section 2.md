## Steps to install Nginx 1.23.1 from source without using apt package manager

### Step 1: Install Prerequisites
```
sudo apt-get install build-essential libpcre3 libpcre3-dev zlib1g zlib1g-dev libssl-dev libgd-dev libxml2 libxml2-dev uuid-dev
```
### Step 2: Download Nginx Package
```
wget http://nginx.org/download/nginx-1.23.1.tar.gz
```
### Step 3: Extract Tar Ball
```
tar -zxvf nginx-1.23.1.tar.gz
```
### Step 4: Navigate to Source Code Folder
```
cd nginx-1.23.1
```
### Step 5: Configure the Build with Necessary Options
```
./configure --prefix=/var/www/html --sbin-path=/usr/sbin/nginx --conf-path=/etc/nginx/nginx.conf --http-log-path=/var/log/nginx/access.log --error-log-path=/var/log/nginx/error.log --with-pcre  --lock-path=/var/lock/nginx.lock --pid-path=/var/run/nginx.pid --with-http_ssl_module --with-http_image_filter_module=dynamic --modules-path=/etc/nginx/modules --with-http_v2_module --with-stream=dynamic --with-http_addition_module --with-http_mp4_module
```
### Step 6: Compile NGINX Source Code
```
make
```
### Step 7: Install the Compiled Source Code
```
sudo make install
```
### Step 8: Start Nginx Server
```
sudo nginx
```
## Steps to configure example.com on installed webserver 

### step 1: Create a directory and index.html file
```
sudo mkdir -p /var/www/example.com
sudo nano /var/www/example.com/index.html
```
### step 2: Insert sample code in index.html 
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Welcome to example.com</title>
</head>
<body>
    <h1>Hello, example.com!</h1>
    <p>This is a sample HTML website hosted on Nginx.</p>
</body>
</html>
```
### step 3: Edit nginx.conf file for load balancing 
```
sudo nano /etc/nginx/nginx.conf
```

### step 4:- Replace the default content with given code 
```
http {
    upstream backend {
        server 10.12.0.1;
        server 10.13.0.1;
        # These are my local ip address. 
    }

    server {
        listen 80;
        server_name example.com;

        location / {
            proxy_pass http://backend;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
        }
    }
}
```
save and close file 
### step 5:- Check nginx configureation 
```
sudo nginx -t
```

## setep 6:- Reload nginx service to make new configuration effactive
```
sudo systemctl restart nginx
```

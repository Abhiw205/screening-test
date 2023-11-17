
## Step 1: Install Prerequisites
sudo apt-get install build-essential libpcre3 libpcre3-dev zlib1g zlib1g-dev libssl-dev libgd-dev libxml2 libxml2-dev uuid-dev

## Step 2: Download Nginx Package
wget http://nginx.org/download/nginx-1.23.1.tar.gz

## Step 3: Extract Tar Ball
tar -zxvf nginx-1.23.1.tar.gz

## Step 4: Navigate to Source Code Folder
cd nginx-1.23.1

## Step 5: Configure the Build with Necessary Options
./configure --prefix=/var/www/html --sbin-path=/usr/sbin/nginx --conf-path=/etc/nginx/nginx.conf --http-log-path=/var/log/nginx/access.log --error-log-path=/var/log/nginx/error.log --with-pcre  --lock-path=/var/lock/nginx.lock --pid-path=/var/run/nginx.pid --with-http_ssl_module --with-http_image_filter_module=dynamic --modules-path=/etc/nginx/modules --with-http_v2_module --with-stream=dynamic --with-http_addition_module --with-http_mp4_module

## Step 6: Compile NGINX Source Code
make

## Step 7: Install the Compiled Source Code
sudo make install

## Step 8: Start Nginx Server
sudo nginx

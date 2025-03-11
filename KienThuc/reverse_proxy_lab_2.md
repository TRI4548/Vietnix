# Mô hình:

![ảnh](https://github.com/user-attachments/assets/221270cc-04c7-4836-9ea4-572d332d2650)

# Mục tiêu: tạo 2 site wp.tringuyen.space và laravel.tringuyen.space
- Với NGINX reverse proxy ở frontend để phục vụ cho việc tải nhanh chóng các static content đến người dùng, không phải thông qua web server apache 
- Web server APACHE ở backend chỉ thực hiện việc yêu cầu các lệnh truy vấn ngôn ngữ PHP

# Các bước thực hiện:

1. Cài httpd (APACHE) và cấu hình cho APACHE từ port 80 sang 8080 để port 80 cho NGINX chạy

```
dnf install httpd -y

nano /etc/httpd/conf/httpd.conf

# Thay đổi thông số sau:

LISTEN 80

# thành

LISTEN 8080

# Ctrl + X để Save lại
```

2. Tạo 2 thư mục cho 2 site wp.tringuyen.space và laravel.tringuyen.space ở /var/www/

```
mkdir /var/www/wp.tringuyen.space
mkdir /var/www/laravel.tringuyen.space
```

3. Tạo 2 file virtual host ở APACHE

```
nano /etc/httpd/conf.d/wp.tringuyen.space.conf

# Nội dung

<VirtualHost *:8080>
	ServerAdmin admin@wp.tringuyen.space
	DocumentRoot /var/www/wp.tringuyen.space/
	ServerName wp.tringuyen.space
	#ServerAlias www.wp.tringuyen.space
	ErrorLog /var/log/httpd/wp.tringuyen.space-error.log
	CustomLog /var/log/httpd/wp.tringuyen.space-access.log combined
</VirtualHost>

-------------------------------------------------------------------------------
nano /etc/httpd/conf.d/wp.tringuyen.space.conf

# Nội dung

<VirtualHost *:8080>
	ServerAdmin admin@laravel.tringuyen.space
	DocumentRoot /var/www/laravel.tringuyen.space/
	ServerName laravel.tringuyen.space
	#ServerAlias www.laravel.tringuyen.space
	ErrorLog /var/log/httpd/laravel.tringuyen.space-error.log
	CustomLog /var/log/httpd/laravel.tringuyen.space-access.log combined
</VirtualHost>
```

4. Cài 2 phiên bản PHP 7.4 cho site wp.tringuyen.space và PHP 8.2 cho site laravel.tringuyen.space

```
# Lệnh này để liệt kê các phiên bản PHP có sẵn để cài đặt
dnf module list php

# Cài PHP 7.4
sudo dnf module reset php
sudo dnf module enable php:remi-7.4
sudo dnf install php74 php74-php-fpm -y

# Cài PHP 8.2
sudo dnf module reset php
sudo dnf module enable php:remi-8.2
sudo dnf install php82 php82-php-fpm -y

# Start dịch vụ và khởi chạy cùng hệ thống khi khởi động
sudo systemctl start php74-php-fpm
sudo systemctl enable php74-php-fpm

sudo systemctl start php82-php-fpm
sudo systemctl enable php82-php-fpm
```

5. Điều chỉnh 2 file vHost để có thể chạy đúng bản PHP

```
nano /etc/httpd/cond.d/wp.tringuyen.space

# Nội dung

<VirtualHost *:8080>
        ServerAdmin admin@wp.tringuyen.space
        DocumentRoot /var/www/wp.tringuyen.space/wordpress
        ServerName wp.tringuyen.space
        #ServerAlias www.wp.tringuyen.space
        ErrorLog /var/log/httpd/wp.tringuyen.space-error.log
        CustomLog /var/log/httpd/wp.tringuyen.space-access.log combined

# Thêm các dòng IfModule chạy PHP 7.4
        <IfModule !mod_php7.c>
                <FilesMatch \.(php|phar)$>
                SetHandler "proxy:unix:/var/opt/remi/php74/run/php-fpm/www.sock|fcgi://localhost"
                </FilesMatch>
        </IfModule>
</VirtualHost>

nano /etc/httpd/cond.d/wp.tringuyen.space

# Nội dung

<VirtualHost *:8000> # app laravel sẽ chạy port 8000
        ServerAdmin admin@laravel.tringuyen.space
        DocumentRoot /var/www/laravel.tringuyen.space/laravel-app
        ServerName laravel.tringuyen.space
        #ServerAlias www.laravel.tringuyen.space
        ErrorLog /var/log/httpd/laravel.tringuyen.space-error.log
        CustomLog /var/log/httpd/laravel.tringuyen.space-access.log combined

# Thêm các dòng IfModule chạy PHP 8.2
        <IfModule !mod_php8.c>
                <FilesMatch \.(php|phar)$>
                SetHandler "proxy:unix:/var/opt/remi/php82/run/php-fpm/www.sock|fcgi://localhost"
                </FilesMatch>
        </IfModule>
</VirtualHost>
```

6. Cài và cấu hình Database (MariaDB)

```
# Cài DB
sudo dnf install mariadb-server mariadb

# Start và khởi chạy DB cùng hệ thống
sudo systemctl start mariadb
sudo systemctl enable mariadb

# Cấu hình DB
sudo mysql_secure_installation
```

7. Tạo các Database cho site Wordpress và Laravel

```
# Tạo cho site wp.tringuyen.space

mysql -u root -p

CREATE DATABASE wordpress_db;
CREATE USER 'wordpress_tringuyen'@'%' IDENTIFIED BY 'DB_password';

GRANT ALL ON wordpress_db.* TO 'wordpress_tringuyen'@'%';
FLUSH PRIVILEGES;
EXIT;

# Tạo cho site laravel.tringuyen.space

mysql -u root -p

CREATE DATABASE laravel_db;
CREATE USER 'laravel_tringuyen'@'%' IDENTIFIED BY 'DB_password';

GRANT ALL ON laravel_db.* TO 'laravel_tringuyen'@'%';
FLUSH PRIVILEGES;
EXIT;
```

8. Cài WordPress

```
cd /var/www/wp.tringuyen.space/

sudo wget https://wordpress.org/latest.tar.gz

sudo tar -xvzf latest.tar.gz

# Truy cập web wp.tringuyen.space:8080 để cài đặt
```

9. Cài Laravel

```
# Cài composer

# Tạo project Laravel
cd /var/www/laravel.tringuyen.space
composer create-project laravel/laravel-app

cd laravel-app
# Tạo project Laravel và xuất output vào file nohup.out
nohup php artisan serve > nohup.out 2>&1 &

# Truy cập web laravel.tringuyen.space:8000 để kiểm tra

# cấu hình DB cho laravel
nano .env

# Khai báo database, database user và password sau đó Save lại

# Dùng lệnh này để lưu vào DB
php artisan migrate

```

10. Cài NGINX:

```
dnf install nginx -y
```

Cấu hình 2 NGINX block

```
nano /etc/nginx/conf.d/wp.tringuyen.space.conf

# Nội dung

server {
    listen 80;
    server_name wp.tringuyen.space;

    # Khai báo chỗ này để NGINX phục vụ các static content đến người dùng
    location ~* \.(jpg|jpeg|png|gif|ico|css|js)$ {
        root /var/www/wp.tringuyen.space;
        index index.html index.htm;
        try_files $uri $uri/ =404;  # Serve 404 if file not found
    }

    # Khai báo chỗ này để xử lý các request khác đến APACHE
    location / {
        proxy_pass http://localhost:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    error_page 500 502 503 504 /50x.html;
    location = /50x.html {
        root /usr/share/nginx/html;
    }

}

# Sau đó Save lại

# Cấu hình tương tự với Laravel
nano /etc/nginx/conf.d/laravel.tringuyen.space.conf

# Nội dung

server {
    listen 80;
    server_name laravel.tringuyen.space;

    # Khai báo chỗ này để NGINX phục vụ các static content đến người dùng
    location ~* \.(jpg|jpeg|png|gif|ico|css|js)$ {
        root /var/www/laravel.tringuyen.space;
        index index.html index.htm;
        try_files $uri $uri/ =404;  # Serve 404 if file not found
    }

    # Khai báo chỗ này để xử lý các request khác đến APACHE
    location / {
        proxy_pass http://localhost:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    error_page 500 502 503 504 /50x.html;
    location = /50x.html {
        root /usr/share/nginx/html;
    }

}

# Sau đó Save lại
```

11. Kiểm tra lại syntax apache và nginx

```
apachectl configtest

# Kết quả như này là ổn
Syntax OK

nginx -t

# Kết quả như này là ổn
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```

12. Restart dịch vụ và kiểm tra

```
systemctl restart httpd
systemctl restart nginx
```

13. Cài SSL cho 2 site trên

```
# Cài đặt Certbot
dnf install -y certbot python3-certbot-nginx

# Tạo SSL cho 2 site
certbot --nginx -d wp.tringuyen.space
certbot --nginx -d laravel.tringuyen.space

# Kiểm tra lại bằng cách vào từng site trên web, nếu bị lỗi mất CSS thì đổi file cấu hình trong DocRoot của từng site sao cho chuyển từ http sang https

# Khắc phục site Wordpress bị mất CSS (https://stackoverflow.com/questions/45520972/wordpress-installation-is-missing-style-css/48573044)
```

14. Kiểm tra 2 site có SSL hay chưa

![ảnh](https://github.com/user-attachments/assets/9ecce58c-4b0f-44bc-a820-07b4530dbacd)


![ảnh](https://github.com/user-attachments/assets/7648ecfa-ad05-4e7c-903e-7dfa8b83324c)


15. Test dịch vụ thông qua nginx log và apache log

```
# Thực hiện tải 1 file vào thư mục docroot của site wp.tringuyen.space và thử truy cập
sudo wget https://upload.wikimedia.org/wikipedia/commons/thumb/c/c5/Nginx_logo.svg/1280px-Nginx_logo.svg.png -O /var/www/wp.tringuyen.space/wordpress/nginx-logo.png

https://wp.tringuyen.space/nginx-logo.png
```

Kết quả access log của APACHE

![ảnh](https://github.com/user-attachments/assets/0238299c-d62a-4066-bf2e-0f79c871e077)


Kết quả access log của NGINX

![ảnh](https://github.com/user-attachments/assets/a2297c4b-4c5e-4768-a855-bcc4470b4be3)

=> Ta thấy được file hình ảnh đã được NGINX serve tới người dùng, APACHE chỉ thực hiện các truy vấn php, giúp giảm tải server


16. Cấu hình caching ở NGINX

- Khai báo nơi lưu Cache Zone trong file cấu hình nginx

```
nano /etc/nginx/nginx.conf

# Thêm dòng này trong block http

proxy_cache_path /var/cache/nginx levels=1:2 keys_zone=my_cache:10m max_size=1g inactive=60m use_temp_path=off;
```

- Apply nội dung sau đây vào site wp.tringuyen.space trong NGINX block trong mục location /

```
    proxy_cache my_cache;
    proxy_cache_valid 200 1h;  # Cache 200 responses for 1 hour
```

# Các nguồn tham khảo:
1. [Digital Ocean](https://www.digitalocean.com/community/tutorials/how-to-configure-nginx-as-a-web-server-and-reverse-proxy-for-apache-on-one-ubuntu-18-04-server#step-10-blocking-direct-access-to-apache-optional)
2. [dev.to](https://dev.to/imsushant12/serving-static-content-with-nginx-26ih)
3. [xtom.com](https://xtom.com/blog/how-to-setup-nginx-apache-reverse-proxy-almalinux-rocky-linux/)

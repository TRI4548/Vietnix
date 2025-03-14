# Mô hình:

![ảnh](https://github.com/user-attachments/assets/221270cc-04c7-4836-9ea4-572d332d2650)

# Mục tiêu: tạo 2 site wordpress.tri.vietnix.tech và laravel.tri.vietnix.tech
- Với NGINX reverse proxy ở frontend để phục vụ cho việc tải nhanh chóng các static content đến người dùng, không phải thông qua web server apache 
- Web server APACHE ở backend chỉ thực hiện việc yêu cầu các lệnh truy vấn ngôn ngữ PHP

# Các bước thực hiện (trên AlmaLinux 9):

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

2. Tạo 2 thư mục cho 2 site wordpress.tri.vietnix.tech và laravel.tri.vietnix.tech ở /var/www/

```
mkdir /var/www/wordpress.tri.vietnix.tech
mkdir /var/www/laravel.tri.vietnix.tech
```

3. Tạo 2 file virtual host ở APACHE

```
nano /etc/httpd/conf.d/wordpress.tri.vietnix.tech.conf

# Nội dung

<VirtualHost *:8080>
	ServerAdmin admin@wordpress.tri.vietnix.tech
	DocumentRoot /var/www/wordpress.tri.vietnix.tech/
	ServerName wordpress.tri.vietnix.tech
	#ServerAlias www.wordpress.tri.vietnix.tech
	ErrorLog /var/log/httpd/wordpress.tri.vietnix.tech-error.log
	CustomLog /var/log/httpd/wordpress.tri.vietnix.tech-access.log combined
</VirtualHost>

-------------------------------------------------------------------------------
nano /etc/httpd/conf.d/laravel.tri.vietnix.tech.conf

# Nội dung

<VirtualHost *:8080>
	ServerAdmin admin@laravel.tri.vietnix.tech
	DocumentRoot /var/www/laravel.tri.vietnix.tech/laravel-app/public
	ServerName laravel.tri.vietnix.tech
	#ServerAlias www.laravel.tri.vietnix.tech
	ErrorLog /var/log/httpd/laravel.tri.vietnix.tech-error.log
	CustomLog /var/log/httpd/laravel.tri.vietnix.tech-access.log combined
</VirtualHost>
```

4. Cài PHP 7.4

```
# Lệnh này để liệt kê các phiên bản PHP có sẵn để cài đặt
dnf module list php

# Cài PHP 7.4
sudo dnf module reset php
sudo dnf module enable php:remi-7.4
sudo dnf install php74 -y
```

5. Điều chỉnh 2 file vHost để có thể chạy đúng bản PHP

```
nano /etc/httpd/cond.d/wordpress.tri.vietnix.tech

# Nội dung

<VirtualHost *:8080>
        ServerAdmin admin@wordpress.tri.vietnix.tech
        DocumentRoot /var/www/wordpress.tri.vietnix.tech/wordpress
        ServerName wordpress.tri.vietnix.tech
        #ServerAlias www.wordpress.tri.vietnix.tech
        ErrorLog /var/log/httpd/wordpress.tri.vietnix.tech-error.log
        CustomLog /var/log/httpd/wordpress.tri.vietnix.tech-access.log combined
</VirtualHost>

=====================================================================================

nano /etc/httpd/cond.d/laravel.tri.vietnix.tech

# Nội dung

<VirtualHost *:8080>
        ServerAdmin admin@laravel.tri.vietnix.tech
        DocumentRoot /var/www/laravel.tri.vietnix.tech/laravel-app
        ServerName laravel.tri.vietnix.tech
        #ServerAlias www.laravel.tri.vietnix.tech
        ErrorLog /var/log/httpd/laravel.tri.vietnix.tech-error.log
        CustomLog /var/log/httpd/laravel.tri.vietnix.tech-access.log combined
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
# Tạo cho site wordpress.tri.vietnix.tech

mysql -u root -p

CREATE DATABASE wordpress_db;
CREATE USER 'wordpress_tringuyen'@'%' IDENTIFIED BY 'DB_password';

GRANT ALL ON wordpress_db.* TO 'wordpress_tringuyen'@'%';
FLUSH PRIVILEGES;
EXIT;

# Tạo cho site laravel.tri.vietnix.tech

mysql -u root -p

CREATE DATABASE laravel_db;
CREATE USER 'laravel_tringuyen'@'%' IDENTIFIED BY 'DB_password';

GRANT ALL ON laravel_db.* TO 'laravel_tringuyen'@'%';
FLUSH PRIVILEGES;
EXIT;
```

8. Cài WordPress

```
cd /var/www/wordpress.tri.vietnix.tech/

sudo wget https://wordpress.org/latest.tar.gz

sudo tar -xvzf latest.tar.gz

# Truy cập web wordpress.tri.vietnix.tech:8080 để cài đặt
```

9. Cài Laravel

```
# Cài composer

# Tạo project Laravel
cd /var/www/laravel.tri.vietnix.tech
composer create-project laravel/laravel-app

# Truy cập web laravel.tri.vietnix.tech:8080 để kiểm tra

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
nano /etc/nginx/conf.d/wordpress.tri.vietnix.tech.conf

# Nội dung

server {
    listen 80;
    server_name wordpress.tri.vietnix.tech;

    # Khai báo chỗ này để NGINX phục vụ các static content đến người dùng
    location ~* \.(jpg|jpeg|png|gif|ico|css|js)$ {
        root /var/www/wordpress.tri.vietnix.tech;
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
nano /etc/nginx/conf.d/laravel.tri.vietnix.tech.conf

# Nội dung

server {
    listen 80;
    server_name laravel.tri.vietnix.tech;

    # Khai báo chỗ này để NGINX phục vụ các static content đến người dùng
    location ~* \.(jpg|jpeg|png|gif|ico|css|js)$ {
        root /var/www/laravel.tri.vietnix.tech/laravel-app;
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
certbot --nginx -d wordpress.tri.vietnix.tech
certbot --nginx -d laravel.tri.vietnix.tech

# Kiểm tra lại bằng cách vào từng site trên web, nếu bị lỗi mất CSS thì đổi file cấu hình trong DocRoot của từng site sao cho chuyển từ http sang https

# Khắc phục site Wordpress bị mất CSS (https://stackoverflow.com/questions/45520972/wordpress-installation-is-missing-style-css/48573044)
```

14. Kiểm tra 2 site có SSL hay chưa

![image](https://github.com/user-attachments/assets/5999c262-5a61-47f4-a8b0-c337472bcf73)


![image](https://github.com/user-attachments/assets/cd0826b7-def3-47f9-9e05-7b99e1a496ac)


15. Test dịch vụ thông qua nginx log và apache log

```
# Thực hiện tải 1 file vào thư mục docroot của site wordpress.tri.vietnix.tech và thử truy cập
sudo wget https://upload.wikimedia.org/wikipedia/commons/thumb/c/c5/Nginx_logo.svg/1280px-Nginx_logo.svg.png -O /var/www/wordpress.tri.vietnix.tech/wordpress/nginx-logo.png

# Truy cập https://wordpress.tri.vietnix.tech/nginx-logo.png
```

Kết quả access log của APACHE

![image](https://github.com/user-attachments/assets/a31f41aa-3848-4172-b60e-ae99ff393faf)

Kết quả access log của NGINX

![image](https://github.com/user-attachments/assets/83818525-28e2-4f3e-9b1b-ee2dd05e52ea)

=> Ta thấy được file hình ảnh đã được NGINX serve tới người dùng, APACHE chỉ thực hiện các truy vấn php, giúp giảm tải server


16. Cấu hình caching ở NGINX

- Khai báo nơi lưu Cache Zone trong file cấu hình nginx

```
nano /etc/nginx/nginx.conf

# Thêm dòng này trong block http

proxy_cache_path /var/cache/nginx levels=1:2 keys_zone=my_cache:10m max_size=1g inactive=60m use_temp_path=off;
```

- Apply nội dung sau đây vào site wordpress.tri.vietnix.tech trong NGINX block trong mục location /

```
    proxy_cache my_cache;
    proxy_cache_valid 200 1h;  # Cache 200 responses for 1 hour
```

17. Task (không chạy php-fpm)

Quá trình nghiên cứu: 
[Trước khi sử dụng php-fpm thì người ta sử dụng php gì?](https://g.co/gemini/share/f0b81a37d70a) => Chọn DSO (mod_php) vì CGI và FCGI có liên quan đến PHP-FPM

![image](https://github.com/user-attachments/assets/c2026eb0-ef47-4919-8caf-fb504db107a3)

Cấu hình:
1. Gỡ cài đặt php-fpm

```
sudo dnf remove php-fpm -y
```

2. Chuyển từ CGI/FastCGI Server API (do có liên quan đến php-fpm) sang DSO (mod_php) 
([Nguồn](https://serverfault.com/questions/318084/how-to-switch-from-cgi-fastcgi-server-api-to-dso))

```
# Tìm libphp7.so có trong hệ thống hay không

sudo find / -name "libphp7.so"

# Thêm các dòng này vào file cấu hình của httpd (/etc/httpd/conf/httpd.conf)

LoadModule php7_module  modules/libphp7.so
AddHandler php7-script  .php 
```

3. Reload lại httpd thì bị báo lỗi AH00534: httpd: Configuration error: No MPM loaded.

![image](https://github.com/user-attachments/assets/019f5008-990c-4b38-9b8b-95a11defcfdb)


Cách khắc phục: https://www.linuxquestions.org/questions/slackware-14/ah00534-httpd-configuration-error-no-mpm-loaded-4175499888-print/

Vị trí file: /etc/httpd/conf.modules.d/00-mpm.conf

4. Reload lại service http

5. Kiểm tra php chạy DSO hay chưa: kiểm tra bằng tạo file info.php

![image](https://github.com/user-attachments/assets/324816bf-d10d-421f-958f-cffea5c29743)

![image](https://github.com/user-attachments/assets/0e083709-5fa9-4200-a08a-9872e9ab63b8)


# Các nguồn tham khảo:
1. [Digital Ocean](https://www.digitalocean.com/community/tutorials/how-to-configure-nginx-as-a-web-server-and-reverse-proxy-for-apache-on-one-ubuntu-18-04-server#step-10-blocking-direct-access-to-apache-optional)
2. [dev.to](https://dev.to/imsushant12/serving-static-content-with-nginx-26ih)
3. [xtom.com](https://xtom.com/blog/how-to-setup-nginx-apache-reverse-proxy-almalinux-rocky-linux/)

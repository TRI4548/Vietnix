Mô hình:

Tạo web server apache trên almalinux với 2 website lần lượt là wp.tringuyen.space và laravel.tringuyen.space trỏ về localhost:8080 

Với Nginx làm reverse proxy ở phía trước thì người dùng nhập wp.tringuyen.space sẽ hiển thị "Site 1" còn laravel.tringuyen.space sẽ hiển thị "Site 2"

Các bước thực hiện:

1. cài httpd (apache)

```
dnf install httpd -y
```

2. Tạo 2 thư mục cho 2 site wp.tringuyen.space và laravel.tringuyen.space ở /var/www/

```
mkdir /var/www/wp.tringuyen.space
mkdir /var/www/laravel.tringuyen.space
```

3. Tạo 2 file virtual host

```
touch /etc/httpd/conf.d/wp.tringuyen.space.conf
touch /etc/httpd/conf.d/wp.tringuyen.space.conf
```

4. Nhập nội dung như sau cho các file trên:

```
<VirtualHost *:8080>
	ServerAdmin admin@wp.tringuyen.space
	DocumentRoot /var/www/wp.tringuyen.space/
	ServerName wp.tringuyen.space
	#ServerAlias www.wp.tringuyen.space
	ErrorLog /var/log/httpd/wp.tringuyen.space-error.log
	CustomLog /var/log/httpd/wp.tringuyen.space-access.log combined
</VirtualHost>
```

Tương tự với laravel.tringuyen.space

5. Đổi apache từ port 80 sang 8080 và đổi luôn 2 port của vhost thành 8080 (nano /etc/httpd/conf/httpd.conf)

```
LISTEN 80 thành 8080
```

Mục đích để chạy apache port 8080 không bị xung đột khi chạy nginx port 80

6. Cài NGINX:

```
dnf install nginx -y
```

Cấu hình 2 vhost (nano /etc/nginx/conf.d/wp.tringuyen.space.conf và nano /etc/nginx/conf.d/laravel.tringuyen.space.conf)

```
server {
    listen 80;
    server_name wp.tringuyen.space;

    location / {
        proxy_pass http://localhost:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

tương tự với laravel.tringuyen.space

chỗ **proxy_pass** sẽ khai báo server backend mà nginx sẽ giao tiếp để lấy nội dung gửi lại cho người dùng

7. Kiểm tra lại syntax apache và nginx

```
apachectl configtest
nginx -t
```

8. Restart dịch vụ và kiểm tra

```
systemctl restart httpd
systemctl restart nginx
```

![ảnh](https://github.com/user-attachments/assets/127a41e5-1aad-44ac-847e-ed612964fbf7)

![ảnh](https://github.com/user-attachments/assets/af603c4b-daf5-41dc-89b2-f7ac9fe76966)


